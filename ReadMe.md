
# Migrations

```
enable-migrations
```

```
add-migration CommitMessage
```

**CommitMessage**: Represents the change being made to the migration files.

To add a custom model to the database migration context, it needs to be added like this in the following file:

./Models/Customers.cs
./Models/IdentityModels.cs : ApplicationDbContext

```
public DbSet<ClassName> TableName { get; set; }
public DbSet<Customers> Customers { get; set; }
```

After you've added the custom models for the first time, rewrite the initial database migration model:

```
add-migration CommitMessage -force
```

Once it's added, update the database with:

```
update-database
```

A new .mdf file will appear in the folder./App_Data, if it's hidden click on the option to show all files.
The first time it's generated it won't be associated with the project, right click on it and then click on the Associate option.

To see the data in the database double click on the same file. This will open the Servers Explorer.

## Add a foreign key:

```
public class Customers
{
    public int Id { get; set; }
    public string Name { get; set; }
    public bool NewsletterSubscription { get; set; }    
    public byte MembershipTypeId { get; set; }
    public virtual MembershipType MembershipType { get; set; }  
}

public class MembershipType
{
    public byte Id { get; set; }
    [Required]
    public string Name { get; set; }
    public short SignUpFee { get; set; }
    public byte DurationInMonths { get; set; }
    public byte DiscountRate { get; set; }

    public static readonly byte Unknown = 0;
    public static readonly byte PayAsYouGo = 1;
}
```
