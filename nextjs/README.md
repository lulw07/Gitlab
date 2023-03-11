# Nextjs Pipeline

Here you will find all necessary pipline files to create a nextjs application.

In the Dockerfile you can see that I got all my files in the /src directory.

My project structure looks like this:

```
Nextjs-Project
├─ .gitlab.ci.yml
├─ Dockerfile
├─ README.md
├─ src/
│  ├─ pages/
│       └─ ...
│  ├─ public/
│       └─ ...
│  └─ styles/
│       └─ ...
├─ .gitignore
├─ next.config.js
├─ package-lock.js
└─ package.json
```

On my deployment server I installed the [Nginx-Proxy](https://github.com/nginx-proxy/nginx-proxy) from the official repository and [acme-companion](https://github.com/nginx-proxy/acme-companion) from the nginx-proxy repo.

The acme-companion create automatically a SSL certificate for your Domain. Therefore, you have to point the Domain simply to your server ip-address.