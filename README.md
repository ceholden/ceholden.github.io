Personal website of Chris Holden, hosted using [GitHub Pages](http://pages.github.com).

## Dependencies:

Ruby with Jekyll for Github Pages. From [documentation](https://help.github.com/articles/using-jekyll-with-pages/):

First get `bundler` gem:
``` bash
sudo apt-get install ruby-dev
sudo gem install bundle
```

Next use the Gemfile to manage the Ruby Gems as used on Github Pages:
``` bash
bundle install
```

Finally have Jekyll serve the site locally using the environment setup through `bundle`:
``` bash
bundle exec jekyll serve -w
```
