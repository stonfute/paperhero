
# Tired of browsing directories of pdfs?

This small and hackable applications allows you to store your pdfs locally on your server or desktop pc. It just needs **Python2.7**. There is no database! It is more or less a rewrite of my [old implementation](https://github.com/PatWie/papershelf).

Features:
- download papers directly from Arxiv including meta data
- fuzzy search your local papers
- paper-preview generator

## Get Google-Key
To download papers from arxiv directly you need to aquire a Google developer-key and a custom search-engine-key.

- Goto https://code.google.com/apis/console/?api=plus to generate a new developerkey and 
- then https://console.developers.google.com/apis/api/customsearch/overview?project=<your-project-id> to 

Unfortunately, you are only allowed to send 100 request per day when using the Google-API.

## Install locally
````bash
    # get montage command
    sudo apt-get install imagemagick imagemagick-doc 
    cd /var/www/papers
    git clone https://github.com/PatWie/paperhero.git
    cd paperhero
    pip install -r requirements.txt --user
    mkdir data
    mkdir js
    mkdir css
    python2.7 compile.py # compile sass and minify js
    # ready to start
    python2.7 app.py --port 8888 --cx '0815:foobar' --devkey "morefoobar"
````

Now point your browser to http://localhost:8888

## Install on your VirtualPrivateServer (VPS)

I assume you have already NginX properly configured and running. An example config file is given in [docs](docs). This uses NginX for serving static assets and as a load-balancer for the python app itself.
````bash
    cd paperhero 
    sudo chown -R your-user:your-user .
    sudo cp docs/paperhero.conf /etc/nginx/sites-available/paperhero.conf
    # edit (server-name, path, port)
    sudo nano /etc/nginx/sites-available/paperhero.conf
    # activate site
    sudo ln -s /etc/nginx/sites-available/paperhero.conf /etc/nginx/sites-enabled/
    # start app (in another terminal)
    python2.7 app.py --port 8100 --cx '0815:foobar' --devkey "morefoobar"&
    sudo service nginx reload
````


