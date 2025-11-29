+++
# Basic
title = '{{ replace .File.ContentBaseName "-" " " | title }}'
date = '{{ .Date }}'
lastmod = '{{ .Date }}'
draft = true

# URL
slug = '{{ .File.ContentBaseName | urlize }}'
# url will follow your permalinks setting: '/:year/:month/:slug/'

# SEO
description = ''
# featured image for social cards (optional)
# featuredImage = ''
# image = ''
# noindex = false

# Taxonomy
categories = []
tags = []

# Featured flag
featured = false

# Page options
mermaid = false
toc = false
+++

在这里撰写正文……
