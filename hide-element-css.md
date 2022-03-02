# Hide an element with CSS

1) To hide an element, we will use CSS. First, create a tag "Custom" with name "TC - Hide specific element".

2) Select "Déclencheur(s)" to "Container loaded", and on the dropdownn "Catégorie de Privacy", select "Ne pas inclure dans la privacy".

3) Depending on the website, you must indicate the CSS identifier targeted by the masking.
In this situation, we will hide the element `<div id="message-cookie"></div>` with CSS. Magic ?

3) Put the code and save :

```js
<script type="javascript">
  /***************************************************************************
 * Hide element div#message-cookie defined on source code
 */
(function(){
    try {
        document.head.appendChild(document.createElement("style")).innerHTML="div#message-cookie{visibility:hidden;}";
    } catch (e) {}
})();
</script>
