# Consent management for videos

To manage consent on your video players (ex: Youtube, Vimeo, etc.), I recommend a simple solution to set up.
This solution will allow you to display a message instead of the player, if the user has not given his consent.

NB: In TrustCommander, **I recommend using [vendors](https://community.commandersact.com/trustcommander/user-guides/categories-and-tags/manage-vendors#vendors)**.
This will make it easier to manage consents. Contact support for more setup information.

1) Create a "Features" category and a "Youtube" provider. Don't forget to associate the supplier with this category.
Note the category and vendor IDs.

2) Push this script on your website on pages contained videos. Don't forget to replace category ID and vendor ID with yours :

```js
      <script type="javascript">
        /***************************************************************************
       * Consent management for videos players
       */

        window.caReady = window.caReady || []; 
        window.cact = function() { window.caReady.push(arguments); };

        // We check if consent for videos is obtained, otherwise we display a popin above the player
            window.privacy = window.privacy || {};

            window.privacy.updateYoutubeVideos = () => {
                cact('consent.get', function (result) {
            
                    const FEATURES_ID = 7;
                    const featuresCategory = result.consent.categories[FEATURES_ID] || {};

                    const YOUTUBE_ID = 3;
                    const youtubeVendor = result.consent.vendors[YOUTUBE_ID] || {};
                    
                    if (featuresCategory.status === 'on' && youtubeVendor.status === 'on') {
                        
                        // Consent was provided for the category. 
                        document.querySelectorAll('.block-fixed-popin-youtube').forEach(e => e.style.display = 'none');
                        
                    } else {
                    
                        // Consent was not provided for the category.
                        document.querySelectorAll('.block-fixed-popin-youtube').forEach(e => e.style.display = '');
                        
                    }
                        
                });
            };

            jQuery(document).ready(function(){

                jQuery('.block-fixed-popin-youtube .advanced-link a').on('click', function(e) {
                    e.preventDefault();

                    try {
                        cact('consent.update', {
                            categories: {
                                '7': { status: 'on' }
                            },
                            vendors: {
                                '3': { status: 'on' }
                            }
                        });
                        // Reload popin
                        window.privacy.updateYoutubeVideos();
                    }
                    catch(error) {

                    }
                });
            });

        // Function to re-evaluate consent for videos
        setInterval(function() {
            window.privacy.updateYoutubeVideos();
            }, 2000);
        </script>