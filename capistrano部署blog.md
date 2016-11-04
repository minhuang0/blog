title: rails capistrano 部署自己的blog
date: 2015-04-01
tags: 
    - rails
    - 自动化
categories: 编程

---
把之前写rails blog中的一些笔记迁移过来.
<!--more-->  
下面介绍capistrano版本是'capistrano' 2.12.0的版本,3.x.x的不适用

- 在Gemfile中添加 `gem 'capistrano', '2.12.0'` ，然后后 `Bundle install` 。
- termail输入 `$capify .`会生成 Capfile，config/deploy.rb这两个文件，修改后面deplay.rb 。
- deploy.rb文件主要修改地方IP ,SSH_USER 以及deploy_to 项目路径。
- 文件需要做的内容: 备份原有的项目，上传新的项目，并将重新将软链接指向新部署的项目路径,复制config files到新目录下面,更改public目录文件指向。平缓重启Rails项目
- 配置完成后运行`$bundle exec cap deploy`

下面是我部署的deploy.rb的文件内容.仅供参考.

```
require 'capistrano-rbenv'
load 'deploy/assets'
SSH_USER = 'ubuntu'
ssh_options[:port] = 22
set :rake, "bundle exec rake"
set :application, "huangmin"
set :repository, "."
set :scm, :none
set :deploy_via, :copy



server = "119.254.210.55"

role :web, server
role :app, server
role :db,  server, :primary => true
role :db,  server

set :deploy_to, "/opt/app/huangmin/huangmin_blog"
default_run_options[:pty] = true

# change to your username
set :user, SSH_USER


namespace :deploy do
  task :start do
    run "cd #{release_path} && bundle exec thin start -C config/thin.yml"
  end
  task :stop do
    run "cd #{release_path} && bundle exec thin stop -C config/thin.yml"
  end
  task :restart, :roles => :app, :except => { :no_release => true } do
    db_migrate
    stop
    sleep 2
    start
  end
  task :db_migrate do
    run "cd #{release_path} && bundle install"
    run "cd #{release_path} && bundle exec rake db:create db:migrate RAILS_ENV=production"
  end

  namespace :assets do
    task :precompile do
  #    puts "======= should run precompile"
  #    command = "cd #{release_path} && bundle exec rake RAILS_ENV=production RAILS_GROUPS=assets assets:precompile "
  #    puts "== please run == \n #{command} \n == manually after deploy is done"
      #run "bundle install"
      run "cd #{release_path} && bundle install  && bundle exec rake RAILS_ENV=production RAILS_GROUPS=assets assets:precompile "
    end
  end
end


desc "Copy database.yml to release_path"
task :cp_database_yml do
  puts "=== executing my customized command: "
  run "cp -r #{shared_path}/config/* #{release_path}/config/ "
  run "rm #{release_path}/public/files -rf"
  run "ln -s #{shared_path}/files #{release_path}/public/files "
  # 因为在开发机器上会存在这个文件夹，所以需要先把它删掉，再 ln
  run "rm #{release_path}/public/uploads -rf"
  run "ln -s #{shared_path}/public/uploads #{release_path}/public/uploads"
  puts "=== done (executing my customized command)"
end

before "deploy:assets:precompile", :cp_database_yml
#after "deploy", "deploy:restart"
```
