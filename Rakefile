# Compiles our bootstrap theme
# Derived from http://brizzled.clapper.org/blog/2012/03/05/using-twitter-bootstrap-with-jekyll/

# You need nodejs and npm installed

# npm install less
# gem install uglifier rake

BOOTSTRAP_SOURCE = ENV['BOOTSTRAP_SOURCE'] || File.expand_path("~/bootstrap")
BOOTSTRAP_CUSTOM_LESS = '_less/custom.less'

task :bootstrap_css do |t|
  puts "Copying LESS files"
  Dir.glob(File.join(BOOTSTRAP_SOURCE, 'less', '*.less')).each do |source|
    target = File.join('_less', File.basename(source))
    cp source, target if different?(source, target)
  end

  puts "Compiling #{BOOTSTRAP_CUSTOM_LESS}"
  sh 'lessc', '--compress', BOOTSTRAP_CUSTOM_LESS, 'css/bootstrap.min.css'
end


def different?(path1, path2)
  require 'digest/md5'
  if File.exist?(path1) && File.exist?(path2)
    path1_md5 = Digest::MD5.hexdigest(File.read path1)
    path2_md5 = Digest::MD5.hexdigest(File.read path2)
    (path2_md5 != path1_md5)
  else
    true
  end
end
