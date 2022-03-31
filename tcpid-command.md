# TCPID command

1) To return the TCPID, create a tag "CommandersAct" with name "TC - TCPID command".

2) Select "Déclencheur(s)" to "Container loaded", and on the dropdownn "Catégorie de Privacy", select "Ne pas inclure dans la privacy".

3) Put the code and save :

```js
      <script type="javascript">
        /***************************************************************************
       * Return TCPID w/ the command given in the console:
       * window.alert(tcpid)
       */
      (function(){
        try {
      var getCookie = function(name){
             if(document.cookie.length <= 0)
               return null;
             var regSepCookie = new RegExp('(; )', 'g');
             var cookies = document.cookie.split(regSepCookie);
             for(var i = 0; i < cookies.length; i++){
               var regInfo = new RegExp('=', 'g');
               var infos = cookies[i].split(regInfo);
               if(infos[0] == name){
                 return unescape(infos[1]);
               }
             }
             return null;
            };
            var tcpid = getCookie("TCPID");
        } catch (e){
      }
      })();
      </script>
