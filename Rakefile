require 'html/proofer'

task :build do
  sh "bundle exec jekyll build"
end

task :serve do
  sh "bundle exec jekyll serve"
end

task :htmlproofer do
  HTML::Proofer.new("./_site",
                    {:url_ignore => [/http(s?):\/\/(.*)\.ffka/, /^http:\/\/192\.168\..*/, "https://lists.bl0rg.net/cgi-bin/mailman/listinfo/freifunk-ka"]}).run
end

task :trailing_spaces do
  output = `find pages _posts _sass -type f -exec egrep -l \" +$\" {} \\;`
  if output.strip != "" then
    raise "files containing trailing spaces:\n" + output
  end
end

task :test => :build do
  Rake::Task['trailing_spaces'].invoke
  Rake::Task['htmlproofer'].invoke
end

task :clean do
  sh "bundle exec rm -R ./_site || true"
end

