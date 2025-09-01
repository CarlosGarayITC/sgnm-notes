# Quick Start Guide

## Documenting the Magik Script for Smallworld GIS Data Access

This document describes a Magik script that allows interaction with Smallworld GIS databases and datasets.

### Script Purpose

The objective of this script is to initialize access to Smallworld GIS databases, select a specific database, and list the available collections (tables or feature classes) within that database, showing both their internal names and their external (description) names.

### Quick Copy

For quick interaction with the Magik interpreter, you can copy and paste these code blocks directly.

```
dbs << gis_program_manager.databases
```

```
print(dbs)
```

```
gis_db << dbs[:electric]
```

```
print(gis_db.collections)
```

```
_for collection _over gis_db.collections.fast_elements()
_loop
    write(collection.name, %tab, collection.external_name)
_endloop
```

### Script Steps

Below, each command of the Magik script and its expected output are detailed:

1.  **Initializing GIS Databases**

    This command assigns a reference to the GIS database manager to the global variable `dbs`. If `dbs` does not exist, the system will ask if you want to create it.

    <pre>```
    dbs << gis_program_manager.databases
    ```</pre>

    **Expected Output (if `dbs` does not exist):**

    ```
    Global dbs does not exist: create it? (Y)
    Definiendo global dbs
    ```

2.  **Listing Available Databases**

    To see a list of all configured and accessible GIS databases, copy and paste the following command:

    <pre>```
    print(dbs)
    ```</pre>

    **Expected Output:**

    <pre>```
    hash_table:
    :gnss gnss_dataset(gnss)
    :cymdist gis_ds_view(Cymdist)
    :cis_interface gis_ds_view(Cis_interface)
    :addon gis_ds_view(Addon)
    :electric gis_ds_view(Electric)
    :design_config gis_ds_view(Design_config)
    :design_admin gis_ds_view(Design_admin)
    :task_management gis_ds_view(Task_management)
    :design_work gis_ds_view(Design_work)
    :thematics gis_ds_view(Thematics)
    :dxf gis_ds_view(Dxf)
    :cartografia gis_ds_view(Cartografia)
    :gis gis_ds_view(Gis)
    ```</pre>

    *   **Explanation:** The output shows a `hash_table` where each entry represents a database. For example, `:electric gis_ds_view(Electric)` indicates a database named `electric` with its associated GIS dataset view.

3.  **Selecting a Specific Database**

    This command selects the `electric` database from the available list in `dbs` and assigns it to the global variable `gis_db`. Again, if `gis_db` does not exist, its creation will be prompted.

    <pre>```
    gis_db << dbs[:electric]
    ```</pre>

    **Expected Output (if `gis_db` does not exist):**

    ```
    Global gis_db does not exist: create it? (Y)
    Definiendo global gis_db
    ```

4.  **Listing Collections (Datasets) in the Selected Database**

    To print all collections (which often correspond to "tables" or "feature classes" in a GIS) contained within the `gis_db` database (in this case, `electric`), use the following command:

    <pre>```
    print(gis_db.collections)
    ```</pre>

    **Expected Output (fragment):**

    <pre>```
    hash_table:
    :eo_energy_storage a ds_collection(eo_energy_storage)
    :int!ed_handhole_et_structure_ a ds_collection(int!ed_handhole_et_structure_)
    :schematic_node_annotation a ds_collection(schematic_node_annotation)
    ... (numerous collections)
    ```</pre>

    *   **Explanation:** Similar to the database listing, this output shows a `hash_table` where each entry is a data collection (`ds_collection`) within the `electric` database.

5.  **Iterating and Displaying Collection Names and their Descriptions**

    To list the internal name and external name (description) of each collection in the selected database, copy and paste the following loop:

    <pre>```
    _for collection _over gis_db.collections.fast_elements()
    _loop
        write(collection.name, %tab, collection.external_name)
    _endloop
    ```</pre>

    **Expected Output (fragment):**

    <pre>```
    eo_energy_storage	Almacenamiento de Energía
    int!ed_handhole_et_structure_	int!ed_handhole_et_structure_
    schematic_node_annotation	Schematic Node Annotation
    int!eo_energy_sto_eo_energy_sto2	int!eo_energy_sto_eo_energy_sto2
    ex_dd!version	ex_dd!version
    int!ed_pole_ed_pole_forei	int!ed_pole_ed_pole_forei
    ed_pole_foreign_attachment	Accesorios Exteriores
    data_correction_type	Data Correction Type
    swg_dsn_free_cancellation	Cancelación Libre
    eo_owner_type_name_catalog	Catálogo Nombre de Propiedad
    ... (numerous collections with their descriptions)
    ```</pre>

    *   **Explanation:** This is the most informative part, as it provides a user-readable description of what each internal collection represents. For example, `eo_energy_storage` is described as "Almacenamiento de Energía". Many intermediate or relational collections (`int!...`) may not have a user-friendly external name.

### Conclusion

This Magik script is a fundamental tool for exploring the structure of a Smallworld GIS database, allowing developers and administrators to quickly understand what databases and collections are available and what their purpose is.