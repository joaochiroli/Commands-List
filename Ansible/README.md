# Ansible

## Grupos

- `grupo all` contem todos os hosts explicitamente listados no inventário 

- `ungrouped` contem todos os hosts explicitamente listados no inventário que nao sao membros de grupos

- `grupos aninhados` grupos de grupos

```
[start:end]

[usa]
www.casa[1:2].example.com
192.168.88.[0:255]
```
