# Reload container

1) To reload a container, create a tag "CommandersAct" with name "TC - Privacy Container Reload".

2) On the dropdownn "Catégorie de Privacy", select "Ne pas inclure dans la privacy".

3) Put the code and save :

```js
    <script language="javascript">
    <!--
    // Reload container code
        window.tc_closePrivacyButton = function(){
            tc_action_optin("closePrivacyButton");
        };
        window.tc_closePrivacyCenter = function(type){
             if (type == "save"){
          tc_action_optin("closePrivacyCenter");           
             }
        };
        window.tc_action_optin = function(type){
            if (document.getElementById('tc-privacy-wrapper')){
                var x = document.getElementById('tc-privacy-wrapper');
                document.body.removeChild(x);
            } 
             tC.script.add("https://cdn.tagcommander.com/0000/xyz.js");
        };
    -->
    </script>
    ```
