Consent Manager Installation Instructions

1. Extract the contents of this zip file
2. Place the files in your website directory
3. Add the following code to your HTML page, inside the <head> tag:

<link rel="stylesheet" id="silktide-consent-manager-css" href="path-to-css/silktide-consent-manager.css">
<script src="path-to-js/silktide-consent-manager.js"></script>
<script>
silktideCookieBannerManager.updateCookieBannerConfig({
  background: {
    showBackground: true
  },
  cookieIcon: {
    position: "bottomLeft"
  },
  cookieTypes: [
    {
      id: "noodzakelijk",
      name: "Noodzakelijk",
      description: "<p>Deze cookies zijn noodzakelijk voor een correcte werking van de website en kunnen niet worden uitgeschakeld.﻿</p>",
      required: true,
      onAccept: function() {
        console.log('Add logic for the required Noodzakelijk here');
      }
    },
    {
      id: "advertenties",
      name: "Advertenties",
      description: "<p>Deze website gebruikt de Facebook Pixel om het bezoek te meten en mijn Facebook-advertenties te verbeteren. Door toestemming te geven, help je mij de advertenties relevanter te maken.</p>",
      required: false,
      onAccept: function() {
        gtag('consent', 'update', {
          ad_storage: 'granted',
          ad_user_data: 'granted',
          ad_personalization: 'granted',
        });
        dataLayer.push({
          'event': 'consent_accepted_advertenties',
        });
      },
      onReject: function() {
        gtag('consent', 'update', {
          ad_storage: 'denied',
          ad_user_data: 'denied',
          ad_personalization: 'denied',
        });
      }
    }
  ],
  text: {
    banner: {
      description: "<p>Ik gebruik cookies om het bezoek te meten en mijn Facebook-advertenties te verbeteren. Door cookies te accepteren help je mij de website en advertenties relevanter te maken.</p>",
      acceptAllButtonText: "Alles accepteren",
      acceptAllButtonAccessibleLabel: "Alle cookies accepteren",
      rejectNonEssentialButtonText: "Niet-essentiële weigeren",
      rejectNonEssentialButtonAccessibleLabel: "Weiger niet-essentiële cookies",
      preferencesButtonText: "Voorkeuren",
      preferencesButtonAccessibleLabel: "Voorkeuren wijzigen"
    },
    preferences: {
      title: "Pas je cookievoorkeuren aan",
      description: "<p>Ik respecteer uw privacy. U kunt zelf bepalen welke cookies u toestaat. Uw keuze geldt voor deze hele website.﻿</p>",
      creditLinkText: "Get this banner for free",
      creditLinkAccessibleLabel: "Get this banner for free"
    }
  },
  position: {
    banner: "bottomRight"
  }
});
</script>
