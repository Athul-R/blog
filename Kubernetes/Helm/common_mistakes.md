# Common Mistakes

1. The passing quotes arguments/values to a template.
    This would give `error converting YAML to JSON: yaml: line 21: mapping values are not allowed in this context` as
    the helm would capture the double quotes as well in the values.
    Provide an example here -- the init-containers