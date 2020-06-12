Kiwi IRC can support either reCaptcha or hCaptcha and can always ask for verification or based on dnsbl response

## reCaptcha
To enable reCaptcha support a site key and secret is required from google. These can be obtained [here](https://www.google.com/recaptcha/)
### config.conf
note: *if required = false then [dnsbl] section applies*
```
[verify]
recaptcha_secret = "SECRET KEY HERE"
recaptcha_key = "SITE KEY HERE"

# If required, a client must always pass a captcha challenge before making an IRC connection
required = true
```
### config.json
```
"startupOptions" : {
    "recaptchaSiteId": "SITE KEY HERE",
}
```

## hCaptcha
To enable hCaptcha support a site key and secret key is required from hCaptcha. These can be obtained [here](https://www.hcaptcha.com/)
### config.conf
note: *if required = false then [dnsbl] section applies*
```
[verify]
recaptcha_url = "https://hcaptcha.com/siteverify"
recaptcha_secret = "SECRET KEY HERE"
recaptcha_key = "SITE KEY HERE"

# If required, a client must always pass a captcha challenge before making an IRC connection
required = true
```
### config.json
```
"startupOptions" : {
    "recaptchaURL": "https://hcaptcha.com/1/api.js",
    "recaptchaSiteId": "SITE KEY HERE",
}
```