# Cascade and Specificity

### The cascade rule

When there are same selectors with different declarations, the **later one** is applied due to the **cascade** rule.

```html
<style>
p {
	color: red;
}
p {
    /* only this one will work */
	color: blue;	
}
</style>

<p class="special">What color am I?</p>
```



### Specificity (=우선순위)

A certain order of specificity exists within the CSS cascade rule. 

inline > id > class > selector > inheritance



### Inheritance

Some CSS property values(ex. colors, fonts) set on parent elements are inherited by their child elements. 

Things like widths, margins, padding, and borders do not inherit. 

#### Controlling Inheritance

- `inherit` : literally sets the property value of the selected element to "inherit" its parent (be the same as its parent)
- `initial` : sets the property value to its "default" value
  - ex) `color: initial` == black
- `unset` : resets the property to its natural value (if inherited, the inherited value if not, the initial value)



### !important

`!important` can override most of the rules of cascade. 

- ex) overriding inline css, class over id, etc

but it's best to avoid using !important