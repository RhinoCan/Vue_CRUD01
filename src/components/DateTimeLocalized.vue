<template>
    <div class="DateTime">
        <table>
            <tr><td>{{ formatDateTime }}</td></tr>
        </table>
    </div>
</template>

<script>

export default {
    props: {
        datetime: { type: Date, required: false, default: () => new Date() },
        locale: { type: String, required: false, default: () => 'en-CA' },
        format: { type: String, required: false, default: () => 'DateTime' }
    },
   data() {
       return {
           valid_formats: ["Date", "Time", "DateTime"],
           valid_locales: [
                "ar-SA", //Arabic (Saudi Arabia)
                "bn-BD", //Bangla (Bangladesh)
                "bn-IN", //Bangla (India)
                "cs-CZ", //Czech (Czech Republic)
                "da-DK", //Danish (Denmark)
                "de-AT", //Austrian German
                "de-CH", //"Swiss" German
                "de-DE", //Standard German (as spoken in Germany)
                "el-GR", //Modern Greek
                "en-AU", //Australian English
                "en-CA", //Canadian English
                "en-GB", //British English
                "en-IE", //Irish English
                "en-IN", //Indian English
                "en-NZ", //New Zealand English
                "en-US", //US English
                "en-ZA", //English (South Africa)
                "es-AR", //Argentine Spanish
                "es-CL", //Chilean Spanish
                "es-CO", //Colombian Spanish
                "es-ES", //Castilian Spanish (as spoken in Central-Northern Spain)
                "es-MX", //Mexican Spanish
                "es-US", //American Spanish
                "fi-FI", //Finnish (Finland)
                "fr-BE", //Belgian French
                "fr-CA", //Canadian French
                "fr-CH", //"Swiss" French
                "fr-FR", //Standard French (especially in France)
                "he-IL", //Hebrew (Israel)
                "hi-IN", //Hindi (India)
                "hu-HU", //Hungarian (Hungary)
                "id-ID", //Indonesian (Indonesia)
                "it-CH", //"Swiss" Italian
                "it-IT", //Standard Italian (as spoken in Italy)
                "ja-JP", //Japanese (Japan)
                "ko-KR", //Korean (Republic of Korea)
                "nl-BE", //Belgian Dutch
                "nl-NL", //Standard Dutch (as spoken in The Netherlands)
                "no-NO", //Norwegian (Norway)
                "pl-PL", //Polish (Poland)
                "pt-BR", //Brazilian Portuguese
                "pt-PT", //European Portuguese (as written and spoken in Portugal)
                "ro-RO", //Romanian (Romania)
                "ru-RU", //Russian (Russian Federation)
                "sk-SK", //Slovak (Slovakia)
                "sv-SE", //Swedish (Sweden)
                "ta-IN", //Indian Tamil
                "ta-LK", //Sri Lankan Tamil
                "th-TH", //Thai (Thailand)
                "tr-TR", //Turkish (Turkey)
                "zh-CN", //Mainland China, simplified characters
                "zh-HK", //Hong Kong, traditional characters
                "zh-TW", //Taiwan, traditional characters
           ],
       }
   }, 
   
   computed: {
    formatDateTime() {
        /* Ensure that the locale coming from the parent is valid. */
        if (!this.valid_locales.includes(this.locale)) {
            return "Invalid locale: " + this.locale;
        }

        /* Ensure that the format coming from the parent is valid. */
        if (!this.valid_formats.includes(this.format)) {
            return "Invalid format: " + this.format;
        }
        
        /* Format the Date, Time, or DateTime, depending on what was requested. */
        if (this.format === "Date") {
            return this.datetime.toLocaleDateString(this.locale);
        } else if (this.format === "Time") {  
            return this.datetime.toLocaleTimeString(this.locale);
        } else {
            return this.datetime.toLocaleDateString(this.locale) + "  " +
                this.datetime.toLocaleTimeString(this.locale);    
        }
        },
   }
}
</script>

<style scoped>
@font-face {
    font-family: 'advent_probold';
    src: url('../assets/fonts/adventpro/adventpro-bold-webfont.woff2') format('woff2'),
         url('../assets/fonts/adventpro/adventpro-bold-webfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}
@font-face {
  font-family: 'amaranthbold_italic';
  src: url("../assets/fonts/amaranth/amaranth-bolditalic-webfont.woff2") format("woff2"), 
       url("../assets/fonts/amaranth/amaranth-bolditalic-webfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
}
@font-face {
  font-family: 'arsenalregular';
  src: url("../assets/fonts/arsenal/arsenal-regular-webfont.woff2") format("woff2"), 
       url("../assets/fonts/arsenal/arsenal-regular-webfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
}
td {
    background-color: crimson;
    color: greenyellow;
    font-family: 'arsenalregular', 'advent-probold', 'amaranthbold_italic';
    font-size: 20px; 
    padding: 10px;
} 
.DateTime {
    text-align: left;
}
</style>