Here's a summary of the steps you've taken to create an admin user for your Camunda instance:

### Steps Taken to Create an Admin User in Camunda:

1. **Access the PostgreSQL Database**:

   * You connected to the PostgreSQL container that stores Camunda data with the following command:

   ```bash
   docker exec -it <postgres-container-name> psql -U camunda -d camunda
   ```

2. **Create a New User**:

   * Inserted a new user `admin` with the following details:

     ```sql
     INSERT INTO ACT_ID_USER (ID_, REV_, FIRST_, LAST_, EMAIL_, PWD_)
     VALUES ('admin', 1, 'Admin', 'User', 'admin@camunda.com', 'adminpassword');
     ```

3. **Create a New Group**:

   * Created an admin group named `admin`:

     ```sql
     INSERT INTO ACT_ID_GROUP (ID_, REV_, NAME_, TYPE_)
     VALUES ('adminGroup', 1, 'admin', 'SYSTEM');
     ```

4. **Assign User to the Admin Group**:

   * Initially, attempted to insert the membership using the incorrect column names (`ID_`), but encountered an error because the `ACT_ID_MEMBERSHIP` table used different column names (`user_id_` and `group_id_`).
   * Corrected the query to use the appropriate column names:

     ```sql
     INSERT INTO ACT_ID_MEMBERSHIP (user_id_, group_id_)
     VALUES ('admin', 'adminGroup');
     ```

reset docker with docker compose down
then
docker compose up -d

5. **Exit PostgreSQL**:

   * After successfully adding the admin user and linking them to the admin group, you exited the PostgreSQL shell.

With these steps, the `admin` user has been created and assigned to the `admin` group. You can now log into Camunda with the following credentials:

* **Username**: `admin`
* **Password**: `adminpassword`

This process should allow you to access Camunda's tasklist, cockpit, admin panel, and welcome screen with full administrative privileges.




از این صفحه شروع کنید

http://192.168.100.37:8581/camunda-welcome/

با یوزر دمو رمز دمو بروید داخل


