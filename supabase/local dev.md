[jon youtube](https://www.youtube.com/watch?v=N0Wb85m3YMI)
```sql
pg_dump -h db.gqwesvrevmawyljxhtlf.supabase.co -p 5432 -d postgres -U postgres -f dump.sql
```

```sql
-- inserts a row into public.profiles
create function public.handle_new_user()
returns trigger
language plpgsql
security definer set search_path = public
as $$
begin
  insert into public.profiles (id, raw_user_meta_data)
  values (
  new.id,
  new.raw_user_meta_data
  );
  return new;
end;
$$;

-- trigger the function every time a user is created
create trigger on_auth_user_created
  after insert on auth.users
  for each row execute procedure public.handle_new_user();
```

test 