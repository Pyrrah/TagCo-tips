# Add Cookies link

1) To add a cookie link on footer of a website, create a tag "Custom" with name "TC - Add cookies link".

2) Select "Déclencheur(s)" to "DOM ready", and on the dropdownn "Catégorie de Privacy", select "Ne pas inclure dans la privacy".

3) Depending on the website, you must adapt the code in the "try" brackets.
In this situation, we will add at the end of the list `<ul id="footer">` an entry `<li>` with the hyperlink "Cookies". Easy ?

3) Put the code and save :

```js
<script type="javascript">
  /***************************************************************************
 * Add entry "Cookies" on bottom
 * NB: This method allows display to adblocker users
 */
(function() {
    try {
        if(document.querySelector('a#cookieLink') === null) {
            if (document.querySelector('#footer ul')) {
                document.querySelector('#footer ul').innerHTML = document.querySelector('#footer ul').innerHTML + '<li><a id="cookieLink" href="javascript:tC.privacyCenter.showPrivacyCenter();">Cookies</a></li>';
            }
        }
    } catch (e) {}
})();
</script>
