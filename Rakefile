require 'bundler'
Bundler.require

task :default => :build

MAPPING = %w(
  p3
  p1
  m9
  p2
  p4 p5 p6 p7 p8 p9
  s1 s2 s3 s4 s5 s6 s7 s8 s9
  east south west north
  m1 m2 m3 m4 m5 m6 m7 m8
  white red green
  back
).map.with_index(1) {|e, i| ["layer#{i}", e] }.to_h.freeze

task :build do
  layers = `inkscape --query-all src/tegaki-jan.svg | grep layer`.scan(/(layer\d+)/).flatten
  bar = ProgressBar.create(total: layers.count, format: "%B%e")

  layers.each do |layer|
    system "inkscape src/tegaki-jan.svg -i #{layer} -j -C --export-plain-svg=dist/#{MAPPING.fetch(layer)}.svg"
    bar.increment
  end
end
