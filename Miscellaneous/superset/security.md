## roles

|roles|intro|
|:-|-:|
|admin |Admins have all possible rights, including granting or revoking rights from other users and altering other people’s slices and dashboards.|
|Alpha|Alpha users have access to all data sources, but they cannot grant or revoke access from other users. They are also limited to altering the objects that they own. Alpha users can add and alter data sources.|
|Gamma|They can only consume data coming from data sources they have been given access to through another complementary role. They only have access to view the slices and dashboards made from data sources that they have access to. Currently Gamma users are not able to alter or add data sources. We assume that they are mostly content consumers, though they can create slices and dashboards.|
|sql_lab|The sql_lab role grants access to SQL Lab. Note that while Admin users have access to all databases by default, both Alpha and Gamma users need to be given access on a per database basis.|
|Public|To allow logged-out users to access some Superset features, you can use the PUBLIC_ROLE_LIKE config setting and assign it to another role whose permissions you want passed to this role. For example, by setting PUBLIC_ROLE_LIKE = Gamma in your superset_config.py file, you grant public role the same set of permissions as for the Gamma role. This is useful if one wants to enable anonymous users to view dashboards. Explicit grant on specific datasets is still required, meaning that you need to edit the Public role and add the public data sources to the role manually.|

## row level security

- Using Row Level Security filters (under the Security menu) you can create filters that are assigned to a particular table, as well as a set of roles. If you want members of the Finance team to only have access to rows where department = "finance", you could:
    - Create a Row Level Security filter with that clause (department = "finance")
    - Then assign the clause to the Finance role and the table it applies to