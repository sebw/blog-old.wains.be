


date: 2008-06-05 18:21:30+00:00


# 'Debian : preventing a package from being updated'

categories:
- Debian/Ubuntu
- Linux


**Put a package on hold :**
`echo "${package} hold" | dpkg --set-selections`

**Remove the hold :**
`echo "${package} install" | dpkg --set-selections`

where ${package} is the package name

**Knowing the status of your packages :**
`dpkg --get-selections`
