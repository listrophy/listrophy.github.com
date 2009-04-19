require 'rake/classic_namespace'

HAML = FileList['**/*.haml']
SASS = FileList['**/*.sass']

HTMLDIR = '.'
CSSDIR = 'stylesheets'

HTML = HAML.collect { |fn| File.join(HTMLDIR, File.basename(fn).ext('html'))}
CSS = SASS.collect { |fn| File.join(CSSDIR, File.basename(fn).ext('css'))}

task :default => [:sass, :haml]

task :haml => [HTML]
task :sass => [CSS]

task ''

directory HTMLDIR
directory CSSDIR

rule '.html' => lambda{ |htmlfile| find_haml(htmlfile) } do |t|
  Task[HTMLDIR].invoke
  sh "haml #{t.source} #{t.name}"
end

rule '.css' => lambda{ |cssfile| find_sass(cssfile) } do |t|
  Task[CSSDIR].invoke
  sh "sass #{t.source} #{t.name}"
end

def find_haml(htmlfile)
  base = File.basename(htmlfile, '.html')
  HAML.find { |s| File.basename(s, '.haml') == base }
end

def find_sass(cssfile)
  base = File.basename(cssfile, '.css')
  SASS.find { |s| File.basename(s, '.sass') == base }
end
