 Ansible Role: Lighthouse

Устанавливает Lighthouse (веб-интерфейс для мониторинга ClickHouse) на CentOS 7.

## Important Note

This role **does not install Nginx**. Nginx must be installed separately before using this role.

## Requirements

- CentOS 7
- Ansible 2.9+
- Nginx (pre-installed)
- Git

## Role Variables

### Default Variables (`defaults/main.yml`)

| Variable | Default | Description |
|----------|---------|-------------|
| `lighthouse_repo` | `"https://github.com/VKCOM/lighthouse.git"` | Git repository URL |
| `lighthouse_install_dir` | `"/var/www/lighthouse"` | Installation directory |
| `lighthouse_version` | `"master"` | Git branch/tag to checkout |
| `nginx_user_name` | `"nginx"` | Nginx system user |
| `nginx_conf_dir` | `"/etc/nginx/conf.d"` | Nginx config directory |
| `lighthouse_config_file` | `"lighthouse.conf"` | Nginx config filename |
| `clickhouse_host` | `"localhost"` | ClickHouse server host |
| `clickhouse_port` | `8123` | ClickHouse HTTP port |
| `lighthouse_server_name` | `"_"` | Nginx server name |
| `lighthouse_server_port` | `"80"` | Nginx listen port |

## Dependencies

None, but requires Nginx to be installed.

## Example Playbook

```yaml
- hosts: lighthouse_servers
  pre_tasks:
    - name: Install Nginx
      yum:
        name: nginx
        state: present
    
    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: yes
  
  roles:
    - lighthouse-role
