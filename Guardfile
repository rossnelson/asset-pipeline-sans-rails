
guard 'shell' do
  watch (%r{^source\/javascripts\/.+$}) { `bundle exec rake compile` }
  watch (%r{^source\/stylesheets\/.+$}) { `bundle exec rake compile` }
  watch (%r{^source\/fonts\/.+$}) { `bundle exec rake compile` }
  watch (%r{^source\/images\/.+$}) { `bundle exec rake compile` }
  watch ("Rakefile") { `bundle exec rake compile` }
end
