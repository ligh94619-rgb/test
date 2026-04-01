python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
DLP测试文件 - 包含硬编码的敏感信息
"""

import os
import json

# 数据库配置 - 敏感信息
DATABASE_CONFIG = {
    'host': '10.0.0.1',
    'port': 3306,
    'user': 'admin',
    'password': 'Admin123!',
    'database': 'production',
    'connection_string': 'mysql://admin:Admin123!@10.0.0.1:3306/production'
}

# API密钥 - 敏感信息
API_KEYS = {
    'stripe': 'sk_live_4eC39HqLyjWDarjtT1zdp7dc',
    'google': 'AIzaSyBzXp9zXp9zXp9zXp9zXp9zXp9zXp9',
    'github': 'ghp_1234567890abcdefghijklmnopqrstuv',
    'aws': 'AKIAIOSFODNN7EXAMPLE'
}

# JWT配置
JWT_SECRET = 'my-super-secret-jwt-key-2024'
JWT_TOKEN = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c'

# 用户数据 - 包含个人信息
users = [
    {
        'name': '张三',
        'id_card': '11010119900307663X',
        'phone': '13812345678',
        'email': 'zhang.san@company.com',
        'bank_card': '6217850000012345678'
    },
    {
        'name': '李四',
        'id_card': '32010119850615003X',
        'phone': '15912345678',
        'email': 'li.si@company.com',
        'bank_card': '6222020200123456789'
    }
]

def send_to_server(data):
    """模拟发送数据到服务器"""
    # 敏感数据会被传输
    payload = json.dumps(data)
    # 这里会被DLP拦截
    print(f"Sending data: {payload[:100]}...")
    return True

def upload_file(filename):
    """模拟文件上传"""
    with open(filename, 'r') as f:
        content = f.read()
        # 文件内容包含敏感信息
        send_to_server({'filename': filename, 'content': content})

if __name__ == '__main__':
    # 触发数据传输
    send_to_server(DATABASE_CONFIG)
    send_to_server({'api_keys': API_KEYS})
    upload_file('test_sensitive_data.txt')
