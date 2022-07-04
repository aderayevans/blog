# Fullstack? Why not (Django + Vue-js)

<style>
    r { color: Red }
    g { color: Green }
    b { color: Blue }
    Orange { color: Orange }
    LightGreen { color: LightGreen }
    Cyan { color: Cyan }
    LightPink { color: LightPink }
</style>

## Table of Contents
1. [Django for backend](#django)
2. [Vue.js for frontend](#vuejs)

## <Cyan>Settings essentials</Cyan> 
<hr>

<h2 id="django"><LightGreen>Django for backend</LightGreen></h2>
<hr>
- Anaconda for virtual environment 4.12.0

```python
conda create --name django-env

activate django-env #activate the environment
```

*_Remember to install all commands below inside conda env_ (`django_env`)*

- \>= Python 3.10.4
- Django 4.0.5
> python -m pip install Django

- Django CORS : <Orange>*Cross-Origin-Resource-Policy*</Orange>
> python -m pip install django-cors-headers



<h2 id="vuejs"><LightPink>Vue.js for frontend</LightPink></h2>
<hr>
- Install Nodejs 16.15.1 and npm 8.11.0 at https://nodejs.org/en/download/
- vue-cli 5.0.6
> npm install -g vue-cli

- axios 0.27.2
> npm i axios

- typescript 4.7.4 (when cannot find `{frontend_project_dir}/node_modules/typescript`)
> npm install typescript

or
> npm install -g typescript

## Additional settings:

add this line to `{frontend_project_dir}/jsconfig.json`
```js
    "jsx": "preserve",
```
```js
    {
  "compilerOptions": {
    "target": "es5",
    "jsx": "preserve",
    "module": "esnext",
    "baseUrl": "./",
    "moduleResolution": "node",
    "paths": {
      "@/*": [
        "src/*"
        // "./src/**/*.ts"
      ]
    },
    "lib": [
      "esnext",
      "dom",
      "dom.iterable",
      "scripthost"
    ]
  }
}
```

