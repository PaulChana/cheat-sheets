# Find disabled automations

Paste this in the template editor

```yml
{{ states.automation | selectattr('state', 'eq', 'off') 
   | map(attribute='name') | list | join ('\n') }}
```

#homeassistant 