ASTYLES ONE Rentals — Build 002 + Supabase Storage

Supabase Storage is configured in index.html for the public bucket:
property-images

Photos are uploaded to:
properties/<timestamp>-<uuid>.<extension>

The frontend uses the Supabase anon/publishable key. This key is safe to expose in browser code when Row Level Security / Storage policies are configured correctly. Never put a service_role key in this file.

Required Storage INSERT policy (run once in Supabase SQL Editor if uploads are rejected):

create policy "Allow public property image uploads"
on storage.objects
for insert
to anon, authenticated
with check (bucket_id = 'property-images');

The bucket should remain PUBLIC so uploaded listing photos can be displayed with getPublicUrl().
