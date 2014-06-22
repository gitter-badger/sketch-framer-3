desc "Build script from source"
task :build do
  system("echo '// Export to Framer 3 (ctrl alt cmd f)\n' > 'Export to Framer.sketchplugin'")
  system("echo '(function(){\n' >> 'Export to Framer.sketchplugin'")
  system("cat src/sandbox.js src/view.js src/sketch-framer.js src/metadata.js src/export.js >> 'Export to Framer.sketchplugin'")
  # system("cat src/preamble.js src/sandbox.js src/sketch-framer.js src/export.js >> 'Export to Framer.sketchplugin'")
  system("echo '}())\n' >> 'Export to Framer.sketchplugin'")
end

desc "Run script in Sketch, from coscript"
task :run => :build do
  system("bin/coscript src/run.js 2>/dev/null")
end

desc "Install plugin in all Sketch versions"
task :install => :build do
  if File.exist? "#{ENV['HOME']}/Library/Application Support/com.bohemiancoding.sketch3/Plugins/"
    puts "Installing in Sketch Beta & Nightly"
    system("cp *.sketchplugin '#{ENV['HOME']}/Library/Application Support/com.bohemiancoding.sketch3/Plugins/'")
  end
  if File.exist? "#{ENV['HOME']}/Library/Containers/com.bohemiancoding.sketch3/Data/Library/Application Support/com.bohemiancoding.sketch3/Plugins/"
    puts "Installing in Sketch Release"
    system("cp *.sketchplugin '#{ENV['HOME']}/Library/Containers/com.bohemiancoding.sketch3/Data/Library/Application Support/com.bohemiancoding.sketch3/Plugins/'")
  end
  if File.exist? "/Applications/Framer Generator.app/Contents/Resources/framersketch/"
    puts "Installing in Framer Generator"
    system("cp *.sketchplugin '/Applications/Framer Generator.app/Contents/Resources/framersketch/'")
    system("cp src/run.js '/Applications/Framer Generator.app/Contents/Resources/framersketch/'")
  end
end

task :default => :install
