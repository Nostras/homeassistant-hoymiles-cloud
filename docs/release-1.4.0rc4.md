# 1.4.0rc4 — keep asynchronous settings reads from piling up

Settings reads are asynchronous Hoymiles cloud jobs and can remain pending for several minutes. RC3 could time out after about 10 seconds and then submit a new battery/relay read on the next refresh, potentially creating overlapping jobs.

This release keeps the returned settings job ID and resumes polling the same job on later refreshes. Battery and relay settings reads are also serialized per station because they share the asynchronous settings command queue. Existing cached settings remain available while a job is pending.
