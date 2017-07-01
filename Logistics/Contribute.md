# Contribute using Github
## Install prerequisites

Assuming you are using Ubuntu.
```
sudo apt install npm
sudo npm install gitbook-cli -g
```
There's a weird problem on Ubuntu where `node` is installed as `nodejs` so you have to add a symlink.
```
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

## Modify the book
Checkout the book from Github
```
git clone git@github.com:MRASL/documentation.git
```
If you want to preview locally you can host the book.
```
gitbook serve
```
And then point your browser to `http://localhost:4000`.

When you're done, just commit and push to the master branch and your modifications will show up on https://mrasl.gitbooks.io/documentation/ in no time!
