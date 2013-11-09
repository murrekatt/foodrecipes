require "rubygems"
require "stringex"

## -- Misc Configs -- ##

recipes_dir     = "recipes"   # directory for recipe files


# usage rake new_post[my-new-post] or rake new_post['my new post'] or rake new_post (defaults to "new-post")
desc "Begin a new post in #{recipes_dir}"
task :new_recipe, :title do |t, args|
  if args.title
    title = args.title
  else
    title = get_stdin("Enter a title for your recipe: ")
  end

  mkdir_p "#{recipes_dir}/#{title.to_url}"
  filename = "#{recipes_dir}/#{title.to_url}/recipe.md"
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end
  puts "Creating new recipe: #{filename}"
  open(filename, 'w') do |recipe|
    recipe.puts "# #{title}"
    recipe.puts ""
    recipe.puts "![Dish](dish.jpg)"
    recipe.puts ""
    recipe.puts "## Ingredients"
    recipe.puts ""
    recipe.puts "+ "
    recipe.puts ""
    recipe.puts "## Preparation"
    recipe.puts ""
    recipe.puts "1. "
  end
end


def get_stdin(message)
  print message
  STDIN.gets.chomp
end

def ask(message, valid_options)
  if valid_options
    answer = get_stdin("#{message} #{valid_options.to_s.gsub(/"/, '').gsub(/, /,'/')} ") while !valid_options.include?(answer)
  else
    answer = get_stdin(message)
  end
  answer
end

desc "list tasks"
task :list do
  puts "Tasks: #{(Rake::Task.tasks - [Rake::Task[:list]]).join(', ')}"
  puts "(type rake -T for more detail)\n\n"
end
