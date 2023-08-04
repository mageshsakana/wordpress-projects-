# wordpress-projects-
interview
name: Deploy to Production

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up SSH key
      uses: webfactory/ssh-agent@v0.5.3
      with:
        ssh-private-key: ${{ secrets.YOUR_SSH_PRIVATE_KEY }}

    - name: Deploy to server
      run: |
        ssh user@yourdomain.com 'cd /var/www/html && git pull origin main'
