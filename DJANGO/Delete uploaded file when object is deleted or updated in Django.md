# Delete uploaded file when object is deleted / updated

> 장고에서 첨부파일을 올리면 media 폴더로 가게끔 설정해놨다. 근데 문제는 이미지가 포함된 모델을 삭제해도 내 로컬 media 폴더에 있는 이미지는 **그대로** 남아있음ㅠ 용량차지 어쩔
>
> 그래서 찾아낸 모델 지울 때 실제 첨부파일도 같이 지우기~!

### models.py

```python
from django.db import models

# image resizing
from imagekit.models import ProcessedImageField
from imagekit.processors import Thumbnail

# delete media file
from django.db.models.signals import post_delete, pre_save
from django.dispatch import receiver


class Article(models.Model):

    # 이미지
    image = ProcessedImageField(
        blank=True,
        processors=[Thumbnail(300,300)],
        format='JPEG',
        options={'quality':90},
        upload_to='%Y/%m/%d/'
    )


# 글 삭제할 때 media폴더에 저장된 이미지도 삭제하기
@receiver(post_delete, sender=Article)
def on_delete(sender, instance, **kwargs):
    instance.image.delete(False)


# 수정하고 난 후 그 전에 media 폴더에 있던 이미지도 삭제하기
@receiver(pre_save, sender=Article)
def on_update(sender, instance, **kwargs):
    if not instance.pk:
        return False
    
    try:
        old_img = sender.objects.get(pk=instance.pk).image
    
    except sender.DoesNotExist:
        return False

    new_img = instance.image
    if not old_img == new_img:
        old_img.delete(False)
```

### django.db.models.signals

- defines a set of signals sent by the model system

#### post_delete

- signal sent at the **end** of a model's `delete()` method **and** a queryset's `delete()` method
  - **sender**: the model class
  - **instance** : the actual instance being deleted
- `on_delete()`에서:
  - 특정 Article 인스턴스가 삭제될 때 이 함수로 신호를 보냄
  - 신호 받고 어떤 모델의 어떤 인스턴스인지 확인
  - 그 인스턴스의 **image**(이건 내가 지정한 필드 이름임) 를 삭제시킴

#### pre_save

- signal sent at the beginning of a model's `save()` method
  - **sender**: the model class
  - **instance**:  the actual instance being saved
- `on_update()`에서:
  - 특정 Article 인스턴스가 저장될 때(`save()`함수 시작과 동시에!) 이 함수로 신호가 옴
  - 신호 받으면서 어떤 모델의 어떤 인스턴스인지 확인
  - [if not] 인스턴스에 pk가 없으면? 없는데 어케 삭제함 리턴 폴스
  - [try] 그게 아니라면 현재 신호받은 객체를 `old_image`변수에 담음(pk로 원래 이미지를 찾아내는거)
  - [except] 위에꺼 시도했는데 없거나 sender가 없으면 걍 폴스
  - 여태 리턴 폴스없이 잘 흘러왔으면 지금 새로 들어온 인스턴스의 이미지값을 `new_img`에 받음
  - [if not] 둘이 달라? 그럼 원래있던거 지움