QA Tools for Odoo maintainers
=============================

The goal is to provide helpers to ensure the quality of Odoo addons. 

Sample travis configuration file
---------------------------------

Put this in your project's `.travis.yml`:

    language: python
    python:
      - "2.7"
    
    virtualenv:
      system_site_packages: true
    
    before_install:
     - git clone https://github.com/gurneyalex/maintainer-quality-tools.git $HOME/maintainer-quality-tools
    
    env:
     - PATH=$HOME/maintainer-quality-tools/travis:$PATH
    
    services:
      - postgresql
    
    install:
        - $HOME/maintainer-quality-tools/travis/travis_install_nightly 7.0
        - pip install coveralls flake8
    
    script:
        - travis_run_flake8
        - travis_run_tests 7.0 openerp_test
    
    after_success:
      coveralls

