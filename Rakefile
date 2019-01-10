require "active_support"
require "yaml"

namespace :build do
  task default: :all

  task all: [:rubocop]

  task :rubocop do
    ribose_guide = "src/rubocop/rubocop.ribose.yml"
    thoughtbot_guide = "src/rubocop/rubocop.tb.yml"
    output_guide = "ci/rubocop.yml"
    merge_yaml(thoughtbot_guide, ribose_guide, to: output_guide)
  end

  def merge_yaml(*src, to:)
    aggregation = src.reduce({}) do |acc, file|
      full_path = path_in_project(file)
      y = YAML.safe_load(File.read(full_path))
      acc.deep_merge(y)
    end

    target_full_path = path_in_project(to)
    FileUtils.mkdir_p(File.dirname(target_full_path))
    File.write(to, YAML.dump(aggregation))
    aggregation
  end

  def path_in_project(path)
    File.expand_path(path, __dir__)
  end
end
