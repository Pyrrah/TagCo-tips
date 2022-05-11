# Add Cookies link

## Case 1 : Cookie link don't exist (but footer links `<ul>` exists :smile:)

1) To add a cookie link on footer of a website, create a tag "Custom" with name "TC - Add cookies link".

2) Select "Déclencheur(s)" to "DOM ready", and on the dropdownn "Catégorie de Privacy", select "Ne pas inclure dans la privacy".

3) Depending on the website, you must adapt the code in the "try" brackets.
In this situation, we will add at the end of the list `<ul id="footer">` an entry `<li>` with the hyperlink "Cookies". Easy ?

3) Put the code and save :

```js
<script>
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
```

Alternative (same idea, more lines of code). Don't forget to replace document.querySelector :
```js
<script>
  /***************************************************************************
 * Add entry "Cookies" on bottom
 * NB: This method allows display to adblocker users
 */
(function() {
    try {
        if(document.querySelector('a#cookieLink') === null) {
			var aText = document.createTextNode("Cookies");
			var a = document.createElement('a');
			a.appendChild(aText);
			a.setAttribute("id", "cookieLink");
			a.setAttribute('href','#'+'#');
			a.addEventListener('click', function(event){
				tC.privacyCenter.showPrivacyCenter();
			});
			var li = document.createElement('li');
			li.appendChild(a);
			document.querySelector('#block-menu-block-9 > div > ul.menu.nav').appendChild(li);
        }
    } catch (e) {}
})();
</script>
```

## Case 2 : Footer link exist

Your service provider has created a bad hyperlink for cookies. Ouch.
Don't panic, in this case, we have a solution!

1) To replace the link, create a tag "Custom" with name "TC - Replace cookies link".

2) Select "Déclencheur(s)" to "DOM ready", and on the dropdownn "Catégorie de Privacy", select "Ne pas inclure dans la privacy".

3) Depending on the website, you must adapt the code in the "try" brackets.
In this situation, we will replace the hyperlink `<a class="nav-link">` applied on the text `Cookies`.
Careful, the code only works if this link is unique.

3) Put the code and save :

```js
<script>
  /***************************************************************************
 * Replace "Cookies" on bottom
 * NB: This method allows display to adblocker users
 */
(function() {
try{
  function isCookieLink(element, index, array) {
    return element.innerText.toLowerCase() == "cookies";
  }
  // Return all elements a.nav-link
  var navlink = Array.from(document.querySelectorAll("a.nav-link"));
  // Return cookie link
  var cookieLink = navlink.find(isCookieLink);

  // If we have 1 cookie link
  if (cookieLink!==null || cookieLink.count()<=1) {
    cookieLink.innerHTML = '<a href="javascript:tC.privacyCenter.showPrivacyCenter();">Cookies</a>';
  }
}catch(e){}
})();
</script>
```