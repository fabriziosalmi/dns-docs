# https://community.cloudflare.com/t/recommended-practice-for-migrating-dns/161092

- Do you have DNSSEC? If so, remove the existing records at the registrar unless you know exactly what you are doing, and wait 48 hours.
- Set up your DNS records. If you know what you’re doing do it manually (the import is okay, but has quirks).
- Look for :orange: records, are these just web servers without anything else? If they host anything else switch them to :grey:
- After that you can compare DNS records with dig or a Dig Web Interface 30 tool, compare the results against the nameserver that Cloudflare provides and your existing one, other than the TTL everything should be the same. Check anything that seems important.
- Personally I will set the site to Pause on Cloudflare at this stage and then update the nameservers. Regardless of what goes wrong other than DNSSEC, all you are relying on Cloudflare for is DNS at this stage, so mistakes can be fixed quickly.
- Wait for Cloudflare to recognize the nameserver switch. Also wait until Cloudflare provisions the certificate and then consider either unpausing or set all DNS records to :grey: and just enable a test hostname to :orange: as desired.
- Finally, if and only if everything is good, enable Cloudflare’s DNSSEC and set up the records as needed.
