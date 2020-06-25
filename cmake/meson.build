conf_data = configuration_data()

conf_data.set('YAML_VERSION_MAJOR', '0')
conf_data.set('YAML_VERSION_MINOR', '2')
conf_data.set('YAML_VERSION_PATCH', '5')
conf_data.set('YAML_VERSION_STRING', '0.2.5')

config_file = configure_file(
  input : 'config.h.in',
  output : 'config.h',
  configuration : conf_data
)
