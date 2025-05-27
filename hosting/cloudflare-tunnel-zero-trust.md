
While I have a caddy server that serves HTTPS and reverse proxies all my internal services. I feel somewhat uncomfortable exposing my personal infrastructure directly to the internet at large.

That's why I am using cloudflare tunnel and the built in authentication with cloudflare access for exposing services that are fully exposed to the internet.

To do that I followed these steps:
1. Go to the Zero Trust dasboard
2. Create a Tunnel in Networks -> Tunnels
3. Deploy the docker container with the Tunnel ID
4. Add Github as a Login Method in the Settings -> Authentication
5. Use the Login Method to create an access application
6. Create a policy to only allow certain emails for that access application
    - Be careful about the rules set in the policy. It seems a bit finnicky and adding countries even when valid broke my access for some reason
