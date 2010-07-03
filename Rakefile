require 'open-uri'

YCPATH = ENV['YCPATH'] ||
         ENV['HOME'] + '/local/package/yui/yuicompressor-latest.jar'

SRC = ['init',
       'platform',
       'debug',
       'xmlhttp',
       'json',
       'dom',
       'graphics',
       'date-time',
       'string',
       'html',
       'data-structure',
       'units',
       'ajax',
       'history',
       'window-manager'].map { |x| "scripts/#{x}.js" }

CSS = ['graphics'].map { |x| "styles/#{x}.css" }

task :default => :package

desc "Build package"
task :package => ['simileajax-bundle.js', 'simileajax-bundle.css']

file 'simileajax-bundle.js' => SRC do |t|
  concat(t.prerequisites, t.name)
  yui_compressor(t.name)
end

file 'simileajax-bundle.css' => CSS do |t|
  concat(t.prerequisites, t.name)
  yui_compressor(t.name)
end

def yui_compressor(filename)
  sh "java -jar #{YCPATH} -o #{filename} #{filename}"
  puts "Compressed #{filename}"
end

def concat(srclist, outfile)
  open(outfile, 'w') do |f|
    srclist.each do |src|
      f.write(open(src).read)
      puts "Wrote #{src} to #{outfile}"
    end
  end
end