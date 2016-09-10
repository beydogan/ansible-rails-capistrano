## Ruby on Rails Server Setup with Ansible

1. Update `hosts` file by using your server ip.
2. Update `vars/config.yml` file by your needs.
3. Generate a key pair in `ssh-keys` folder by running `ssh-keygen`. Be careful not to overwrite your own ssh keys. Add this public key to your git repo to use when deploying.
4. Run the playbook by `ansible-playbook setup.yml -i hosts`

You can use capistrano for deployment.


`config/deploy.rb`
```ruby
set :application, 'changeme'
set :repo_url, 'YOUR_GIT_URL'

set :deploy_to, '/data/changeme'
set :linked_files, fetch(:linked_files, []).push('config/database.yml', 'config/secrets.yml', 'config/application.yml')
set :linked_dirs, %w{bin log tmp/pids tmp/cache tmp/sockets vendor/bundle}
after "deploy", "deploy:migrate"
```


`config/deploy/production.rb`

```ruby
set :stage, :production

server 'YOUR_SERVER_IP', user: 'deploy', roles: %w{web app db}
```
