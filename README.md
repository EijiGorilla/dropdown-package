# Introduction

This typescript package is used to generate data in the object-array format for the application to 'react-select'.

Just download as zip and use it (as of November 13, 2023). import fails

# Basic Configuration

```
const dropdownData = new DropDownData({
    featureLayers: [*featureLayer1*, *featureLayer2*] // 2nd feature layer is optional
    fieldNames: [*field1*, *field2*, *field3*] // 2nd and 3rd fields are optional
})

```

# Usage

```
import Select from 'react-select';
import { DropDownData } from './customClass'; // E.g., this package is saved in customClass file.

const [initContractPacakgeCompType, setInitContractPacakgeCompType] = useState([]);

  useEffect(() => {
    const dropdownData = new DropDownData({
      featureLayers: [utilityPointLayer, utilityLineLayer],
      fieldNames: ['CP', 'Company', 'Type'],
    });

    dropdownData.dropDownQuery().then((response: any) => {
      setInitContractPacakgeCompType(response);
    });
  }, []);

    const handleContractPackageChange = (obj: any) => {
    setContractPackage(obj);
    setCompanyList(obj.field2);
    setCompany(null);
    setCompanySelected(obj);
    setType(null);
  };

  const handleCompanyChange = (obj: any) => {
    setCompanySelected(obj);
    setCompany(obj);
    setTypeList(obj.field3);
    setType(null);
  };

  const handleTypeChange = (obj: any) => {
    setType(obj);
  };


  // jsx using react
  return (
    <>
        <Chart
            contractp={contractPackage === null ? '' : contractPackage.field1}
            company={companySelected.name}
            type={type === null ? '' : type}
            typelist={typeList}
        />
    </>

  )

```

## Caution

1. Use esri's feature layers stored in ArcGIS Online or Portal for ArcGIS. Other table formats will fail.
2. You can include only up to two feature layers.
3. You can include only up to three field names (i.e., three dropdown lists)
4. This data format is configured to accommodate specifically 'react-select'.

# dropdown-package
