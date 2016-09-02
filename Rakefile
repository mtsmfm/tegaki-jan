require 'bundler'
Bundler.require

task :default => :build

MAPPING = %w(
  pin_3
  pin_1
  man_9
  pin_2
  pin_4 pin_5 pin_6 pin_7 pin_8 pin_9
  sou_1 sou_2 sou_3 sou_4 sou_5 sou_6 sou_7 sou_8 sou_9
  east south west north
  man_1 man_2 man_3 man_4 man_5 man_6 man_7 man_8
  haku chun hatsu
  back
).map.with_index(1) {|e, i| ["layer#{i}", e] }.to_h.freeze

task :build do
  layers = `inkscape --query-all src/tegaki-jan.svg | grep layer`.scan(/(layer\d+)/).flatten
  bar = ProgressBar.create(total: layers.count, format: "%B%e")

  layers.each do |layer|
    system "inkscape src/tegaki-jan.svg -i #{layer} -j -C --vacuum-defs --export-plain-svg=svg/#{MAPPING.fetch(layer)}.svg"
    bar.increment
  end

  sh "svgo dist"
end
