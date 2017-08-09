require 'rake'

desc "Compile CSS files"
task :clean do
  `rm static/css/style.css`
  `rm static/css/temp.css`
  `rm -rf _site`
end

desc "Compile CSS files"
task :css do
  puts "Merging CSS"

  `rm static/css/style.css`
  `rm static/css/temp.css`

  %W{font-awesome syntax skeleton base layout academicons}.each do |file|
    `cat ./static/css/#{file}.css >> ./static/css/temp.css`
  end

  # `mv ./static/css/temp.css ./static/css/style.css`
  `yuicompressor ./static/css/temp.css > ./static/css/style.css`
  # ruby "compress.rb" # ./static/css/temp.css > ./static/css/style.css
  #`juicer merge ./static/css/temp.css ./static/css/style.css`
  
  `rm static/css/temp.css`
  
  puts 'CSS dumped to ./static/css/style.css'
end

desc "Deploy site"
task :deploy do
  Rake::Task['css'].execute
  puts 'Comitting generated CSS'
  `git add static/css/style.css`
  `git commit -m 'Compressed CSS for deploy'`

  puts "Pushing to Github"
  `git push origin master`
end

desc "Serve"
task :serve do
  Rake::Task['css'].execute

  `open http://localhost:4000`
  `jekyll --serve --no-pygments`
end
