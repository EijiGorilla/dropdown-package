# Introduction

This typescript package is used to generate data using esri's feature layers in the object-array format for the application to 'react-select'.

Just download **index.ts** in src folder as zip and use it (as of November 13, 2023). import fails

# Basic Configuration

```
const dropdownData = new DropDownData({
    featureLayers: [featureLayer1, featureLayer2] // 2nd feature layer is optional
    fieldNames: [field1, field2, field3] // 2nd and 3rd fields are optional
})

Then you need to use Method: dropDownQuery()
See the sample below:

```

# Usage

```
import Select from 'react-select';
import { DropDownData } from './customClass'; // E.g., this package is saved in customClass file.

const [initContractPacakgeCompType, setInitContractPacakgeCompType] = useState([]);
  const [contractPackage, setContractPackage] = useState<any>(null);
  const [company, setCompany] = useState(null);
  const [type, setType] = useState<null | undefined | string>(null);

  const [companyList, setCompanyList] = useState([]);
  const [typeList, setTypeList] = useState([]);
  const [companySelected, setCompanySelected] = useState({ name: '' });

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


  // jsx using react component
  return (
    <>
        <Chart
            contractp={contractPackage === null ? '' : contractPackage.field1}
            company={companySelected.name}
            type={type === null ? '' : type}
            typelist={typeList}
        />

                  <div className="dropdownFilter">
            <div className="dropdownFilterLayout">
              <b style={{ color: 'white', margin: 10, fontSize: '0.9vw' }}></b>
              <Select
                placeholder="Select CP"
                value={contractPackage}
                options={initContractPacakgeCompType}
                onChange={handleContractPackageChange}
                getOptionLabel={(x: any) => x.field1}
                styles={customstyles}
              />
              <br />
              <b style={{ color: 'white', margin: 10, fontSize: '0.9vw' }}></b>
              <Select
                placeholder="Select Company"
                value={company}
                options={companyList}
                onChange={handleCompanyChange}
                getOptionLabel={(x: any) => x.name}
                styles={customstyles}
              />
              <br />
              <b style={{ color: 'white', margin: 10, fontSize: '0.9vw' }}></b>
              <Select
                placeholder="Select Type"
                value={type}
                options={typeList}
                onChange={handleTypeChange}
                getOptionLabel={(x: any) => x.name}
                styles={customstyles}
              />
            </div>
          </div>
    </>

  )

```

## Caution

As of November 13, 2023

1. Use **esri's feature** layers stored in ArcGIS Online or Portal for ArcGIS. Other table formats will fail.
2. You can include only up to two feature layers.
3. You can include only up to three field names (i.e., three dropdown lists)
4. This data format is configured to accommodate specifically 'react-select'.
5. The package does not accommodate select-all options (in the future, this package might include select-all options in dropdown lists).
6. Associated with No.5, when multile dropdown lists are created, these lists are completely cascading (e.g., you need to choose from the first dropdown list in order to choose from the 2nd dropdown list).
