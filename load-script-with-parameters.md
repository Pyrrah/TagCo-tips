# Load a script JS with parameters

Sometimes it is necessary to load JS scripts with particular parameters (specific ID, async load, defer, etc.).
In the example below, you will be able to integrate a specific script according to its environment (prod or recipe).
Let's go :

1) First, create a custom tag with name "TC - Custom JS script".

2) Select "Déclencheur(s)" to "Container loaded", and on the dropdownn "Catégorie de Privacy", select a category.

3) Put the code, custom and save :

```js
    <script>
        // Params
        var id = 'hs-script-loader';
        var src = '';
        var script = document.createElement('script');

        // Select JS source
        if(tC.internalvars.tc_fulldomain === "mybestwebsite.example"){ // Production
            src = 'https://host.example/prod.js';
        } else { // Default: Staging (or other env.)
            src = 'https://host.example/staging.js';
        }

        script.setAttribute('id', id);
        script.setAttribute('src', src);
        script.setAttribute('async', true);     // load asap the script
        script.setAttribute('defer', 'defer');  // don't wait script loaded to build the page

        document.querySelector('body').appendChild(script);

        script.onload = function() {
            // Do whatever you want when it's ready
        }
    </script>
```