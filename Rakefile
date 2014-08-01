#!/usr/bin/env ruby

require 'rubygems'
require 'sprockets'
require 'rubygems'
require 'bundler'
require 'pathname'
require 'logger'
require 'fileutils'
require 'handlebars_assets'

Bundler.require

ROOT        = Pathname.new( File.dirname(__FILE__) )
LOGGER      = Logger.new(STDOUT)
BUILD_DIR   = ROOT.join("build")
SOURCE_DIR  = ROOT.join("source")

BUNDLES     = %w( print.css app.css app.js *.png *.jpg *.svg *.eot *.ttf *.woff )

task :compile do
  sprockets = Sprockets::Environment.new(ROOT) do |env|
    env.logger = LOGGER
  end
  
  AutoprefixerRails.install(sprockets)
  sprockets.append_path HandlebarsAssets.path
  sprockets.append_path(SOURCE_DIR.join('fonts').to_s)
  sprockets.append_path(SOURCE_DIR.join('images').to_s)
  sprockets.append_path(SOURCE_DIR.join('javascripts').to_s)
  sprockets.append_path(SOURCE_DIR.join('stylesheets').to_s)

  Sprockets::Sass.options[:line_comments] = true

  sprockets.each_logical_path(*BUNDLES).each {|path|
    sprockets[path].write_to BUILD_DIR.join(path).to_s
  }

  Rake::Task["notify"].execute
end

task :notify do

  growl = GNTP.new("IM Asset Pipeline")
  growl.register({:notifications => [{
    :name     => "notify",
    :enabled  => true,
  }]})

  growl.notify({
    :name  => "notify",
    :title => "GUARD FILE NOTIFICATION",
    :text  => "Congratulation! Your Assets have been built!",
  })

end  

