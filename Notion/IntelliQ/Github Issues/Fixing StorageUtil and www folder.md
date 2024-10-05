---
Created: 2024-02-09T22:21
Updated: 2024-02-15T01:56
---
- [ ] Development resources should not be included into the installer
    - [ ] package.json
    - [ ] package-lock.json
    - [ ] npm_components
    - [ ] babel_precompile.bat
    - [ ] form_template.jsx
- [ ] Generated forms. Should be put into a temp dir. Path to CSS and scripts should be replaced in the template and should point to files in the installation dir (Program Files, /opt…, etc).
- [ ] Config files. Should be possible for users to edit.
    - [ ] formDef folder
- [ ] Some things to remove:
    - [ ] bower_components/bootstrap
- [ ] Replace CDN link in testspec.ftl to [`http://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css`](http://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css) with the local version to avoid permissions issues?
- [ ] Make locations configurable?
  
# Forms
1. Get temp location for generated forms
2. Get form assets location
3. Get form template location (inside form assets, FormTemplate processor should be aware of its location)
4. Get temp dir.
    1. Get app temp dir
    2. Create a dir for generated forms
    3. Make sure dir is removed on app exit
5. Process form template, emit html form into temp dir.
6. Return html form path to the calling code.
# Getting files when installed
- [ ] Point properties in StorageUtil to different locations
- [ ] Copy formdef contents to the installer