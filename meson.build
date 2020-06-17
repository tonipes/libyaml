project('libyaml', 'c', version : '0.2.', license: 'MIT', default_options : [])

subdir('cmake')

includes = ['include', 'build/cmake']

src = [
    'src/api.c',
    'src/dumper.c',
    'src/emitter.c',
    'src/loader.c',
    'src/parser.c',
    'src/reader.c',
    'src/scanner.c',
    'src/writer.c',
]

libyaml = static_library(
  'libyaml',
  src,
  include_directories : includes,
  c_args : ['-DHAVE_CONFIG_H']
)

libyaml_dep = declare_dependency(include_directories : includes, link_with: libyaml)