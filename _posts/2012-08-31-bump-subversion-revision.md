---
layout: post
title: Bump Subversion Revision
permalink: 2012-08-31-bump-subversion-revision.html
---

This is little powershell script I created to bump the revision number of a subvserion repository by making lots of little commits.

	for ($i=1; $i -le 100; $i++) {
		echo bump$i > bump.txt
		svn ci -m "bump$i"
	}

This will bump 100 revisions.