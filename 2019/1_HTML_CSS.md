# HTML



# CSS

https://estelle.github.io/CSS

## **Cascading**: 

En alttaki öncellikli

## **Specifity**

En belirgin olan öncelikli 

- **!important**(10000pt) > **Inline Style**(1000pt) > **ID**(100pt) > **Class**(10pt) > **tagName**(1pt))
- yukarıdaki sıraya göre override edilir

```css
<style>
h1.main-brand-5 {color: red;} /* 11pt (0,0,0,1,1)*/
.main-brand-5.title-5 {color: orange;} /*20pt (0,0,0,2,0)*/  /*WINS*/
.main-brand-5 {color: green;} /*10pt (0,0,0,1,0)*/
</style>
<h1 class="title-5 main-brand-5">Another Example</h1> 		
```

- Inline styles overrides every outside style
- attribute selectorler class seviyeside


## **Selectors**

- space : descendant
- `>` first level childs
- `+`  sibling the one immediatly after
- `~` siblings(same parent) after  
- `[attrName="val"]` Attribute specific selection
    - `[attrName|="val"]` All values that starts with `val-`
    - `[attrName^="val"]` All values that starts with `val`
    - `[attrName$="val"]` All values that ends with `val`
    - `[attrName~="val"]` All values that includes `val` space seperated
    - `[attrName*="val"]` All values that includes `val` anywhere in that value
- **Structural**
    - `:root` :html tag (document) or svg tag for svg
    - `:first-child`
    - `:last-child`
    - `E:not(s1)` : selection results of E excluding results of selection s1. Specificity of not itself is specificity of s1
    - `:is(div, p) > em` any em item in any div and p == `div > em , p > em`  (not supported for now but will be in the future)

## **Pseudoclasses** and **Pseudoelements**

- **nth-child** formülleri kabul ediyor. **n** -> sıfırdan sonsuza. **sonuç** -> seçilecek olan elemanın sırası (selectorün döndüğü elemanların hepsinin listesi)

```css
li:nth-child(n+6) {color: green;} /*6,7,8.... (ilk beş hariç hepsi)*/
li:nth-child(2n+1) {color: green;} /*1,3,5.... (sıra no tek sayı olanlar)*/
```

```
`last-child` `first-child` `nth-last-child` `nth-first-child`
```

* `::first-line` `::first-letter` (`p:first-child:first-letter`)
*  `::before`  `::after` 
* `:not()` 
  * `input:not([disabled]` 
  * `div:not(.music)` all divs except has music class.
* pseudo class has same specificity weight with class 
* pseudo element has same specificity weight with html tag 



## **Display modes**

- `inline` `block` `inline block` `flex` `inline-flex` `grid` `table` ....  [all](https://developer.mozilla.org/en-US/docs/Web/CSS/display)

- add to every css `{box-sizing: border-box;}` this includes border and padding to width, height etc. calculations.
- flex-basis: size (avarage)

## Flexbox



## Grid



---