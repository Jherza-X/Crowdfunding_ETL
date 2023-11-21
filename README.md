# Crowdfunding_ETL
ETL mini project, UofT Data Visualization BootCamp
Team: Omar Salloum, Ismail Omer, Alexandru Arnautu, Jesus Hernandez

Jupyter Source File: ETL_Mini_Project_OSallou_IOmer_AArnautu_JHernandez.ipynb

Resources folder includes all the cleaning data documents and database squema 
 * The category DataFrame is exported as category.csv
 * The subcategory DataFrame is exported as subcategory.csv
 * The campaign DataFrame is exported as campaign.csv
 * The contacts DataFrame is exported as contacts.csv
 * A database schema labeled, crowdfunding_db_schema.sql


### Import data to database tables code 

engine = create_engine('postgresql://postgres:postgres@localhost/crowdfunding_db')

category_df.to_sql('category', engine, if_exists='append', index=False)
subcategory_df.to_sql('subcategory', engine, if_exists='append', index=False)
contacts_df_clean.to_sql('contacts', engine, if_exists='append', index=False)
campaign_cleaned.to_sql('campaign', engine, if_exists='append', index=False)

### SELECT * statement for each table
tables = ['category', 'subcategory', 'contacts', 'campaign']

def print_tables(table_name):
    with engine.connect() as connection:
        query = f"SELECT * FROM {table_name};"
        result = connection.execute(query)
        columns = result.keys()
        data = result.fetchall()

        print(f"Data for Table: {table_name}")
        print(pd.DataFrame(data, columns=columns))

for table in tables:
    print_tables(table)