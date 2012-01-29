# encoding: UTF-8

$:.unshift("lib")

require 'xcode_build'
require 'xcode_build/output_translator'

class OutputFormatter
  def beginning_translation_of_line(line)
    puts line
  end
  
  def build_started(params)
  end
  
  def build_succeeded
  end
  
  def build_failed
  end
end

class SimpleFormatter
  def build_started(params)
    puts "➜ Build started (#{params.inspect})"
  end
  
  def build_action(params)
    print "."
  end
  
  def build_succeeded
    build_finished
    puts "➜ Build succeeded."
  end
  
  def build_failed
    build_finished
    puts "➜ Build failed."
  end
  
  private
  
  def build_finished
    puts
  end
end

task :clean_example do
  Dir.chdir("resources/ExampleProject") do
    puts "➜ Cleaning"
    XcodeBuild.run("clean", File.open("/dev/null", "w"))
  end
end

task :build_example => :clean_example do
  Dir.chdir("resources/ExampleProject") do
    formatter = SimpleFormatter.new
    XcodeBuild.run("", XcodeBuild::OutputTranslator.new(formatter))
  end
end

task :build_example_and_fail => :clean_example do
  Dir.chdir("resources/ExampleProject") do
    formatter = OutputFormatter.new
    XcodeBuild.run("-configuration AlwaysFails", XcodeBuild::OutputTranslator.new(formatter))
  end
end