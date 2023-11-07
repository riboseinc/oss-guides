# The 'deep_merge()' from 'activesupport' does not merge arrays.
# We need to be able to merge arrays as there are e.g. arrays of rubocop
# plugins from different input guides.
require "deep_merge"
require "yaml"

# Define input and output directories
def dirs(key)
  {
    rubocop: "src/rubocop",
    ci_out:  "ci",
  }[key]
end

# Define input file paths
def input_guides(key)
  {
    ribose: "#{dirs(:rubocop)}/rubocop.ribose.yml",
    thoughtbot: "#{dirs(:rubocop)}/rubocop.tb.yml",
    rails: "#{dirs(:rubocop)}/rubocop.rails.yml",
  }[key]
end

# Define output file paths
def output_guides(key)
  {
    default: "#{dirs(:ci_out)}/rubocop.yml",
    rails: "#{dirs(:ci_out)}/rubocop.rails.yml",
  }[key]
end

# Define input guides for each rubocop flavour
def default_guide_inputs
  %i[thoughtbot ribose]
end

def rails_guide_inputs
  default_guide_inputs + %i[rails]
end

namespace :build do
  task default: :all

  task all: [:rubocop]

  task rubocop: %i[rubocop:default rubocop:rails]

  task :"rubocop:default" do
    merge_yaml_i(*default_guide_inputs, to: output_guides(:default))
  end

  task :"rubocop:rails" do
    merge_yaml_i(*rails_guide_inputs, to: output_guides(:rails))
  end

  def merge_yaml_i(*src, to:)
    merge_yaml(*src.map(&method(:input_guides)), to: to)
  end

  def merge_yaml(*src, to:)
    aggregation = src.reduce({}) do |acc, file|
      full_path = path_in_project(file)
      y = YAML.safe_load(File.read(full_path))
      acc.deep_merge(y)
    end

    target_full_path = path_in_project(to)
    FileUtils.mkdir_p(File.dirname(target_full_path))
    File.write(to, [yaml_header, YAML.dump(aggregation)].join("\n"))
    aggregation
  end

  def path_in_project(path)
    File.expand_path(path, __dir__)
  end

  def yaml_header
    (<<~YAML).chomp
      ############################################
      #       This file is auto-generated.       #
      #           DO NOT EDIT DIRECTLY           #
      #    OR YOUR CHANGES MAY BE OVERWRITTEN    #
      #        Edit source files instead.        #
      #          See README for details.         #
      ############################################
    YAML
  end
end
