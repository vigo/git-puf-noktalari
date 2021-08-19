task :default => [:serve]


desc "Run docs server"
task :serve do
  system "mkdocs serve"
end

desc "Build docs"
task :build do
  system "mkdocs build --clean"
end

desc "Deploy to github"
task :deploy do
  system "mkdocs gh-deploy"
end
