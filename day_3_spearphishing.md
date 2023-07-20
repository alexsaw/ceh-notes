# Day 3

## Spearphishing

## View website with Lynx
```
lynx http://skillsetlocal.com
```

## create folder for company data
```
mkdir targetsite &&
cd targetsite
```

## scrape email addresses from target site
```
wget -q -r http://skillsetlocal.com && grep -E -o -r "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b"
```

