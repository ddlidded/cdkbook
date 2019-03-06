<a name="sec:fileformats"></a>
## File Formats

This appendix lists of file formats the CDK knows about. For each format, it indicated if
the CDK has a reader (R) and/or a writer (W) for it. It also indicates which formats can
be detected from the file content. Chemical file format definitions implementations in
the CDK implement the [`IChemFormatMatcher`](http://cdk.github.io/cdk/latest/docs/api/org/openscience/cdk/io/formats/IChemFormatMatcher.html) class for that.

This script was used to create this list:

**Script** [code/ListAllFileFormats.groovy](code/ListAllFileFormats.code.md)
```groovy
formats = new ArrayList<IChemFormat>();
reader =
  this.getClass().getClassLoader().getResourceAsStream(
    "io-formats.set"
  )
reader.eachLine { formatName ->
  try {
    Class<? extends Object> formatClass =
      this.getClass().getClassLoader().
        loadClass(formatName);
    Method getinstanceMethod =
      formatClass.getMethod(
        "getInstance", new Class[0]
      );
    format = getinstanceMethod.invoke(
      null, new Object[0]
    );
    formats.add(format);
  } catch (ClassNotFoundException exception) {
  } catch (Exception exception) {
  }
}
formats.sort{ it.formatName }
for (format in formats) {
  if (format instanceof IChemFormat &&
      format.getReaderClassName() != null) {
    output.append("R");
  }
  if (format instanceof IChemFormat &&
      format.getWriterClassName() != null) {
    output.append("W");
  }
  if (format instanceof IChemFormatMatcher) {
    output.append("M");
  }
  output.append(format.getFormatName())
}
```

<table>
<tr>
  <td><b>Read/Write</b></td>
  <td><b>Matcher</b></td>
  <td><b>File Format</b></td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>ABINIT</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>ADF</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Aces2</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Alchemy</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Ball and Stick</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>CAChe MolStruct</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>CDK OWL (N3)</td>
</tr>
<tr>
  <td>W</td>
  <td></td>
  <td>CDK Source Code</td>
</tr>
<tr>
  <td>W</td>
  <td></td>
  <td>CML enriched RSS</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>CTX</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Cacao Cartesian</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Cacao Internal</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Chem3D Cartesian 1</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Chem3D Cartesian 2</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>ChemDraw eXchange file</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>Chemical Markup Language</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Chemical Resource Kit 2D</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Chemical Resource Kit 3D</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Chemtool</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>CrystClust</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>Crystallographic Interchange Format</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>DMol3</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Dalton</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Dock 5 Box</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Fenske-Hall Z-Matrix</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Fingerprint</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>GAMESS log file</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>GROMOS96</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>Gaussian 2003</td>
</tr>
<tr>
  <td>W</td>
  <td></td>
  <td>Gaussian Input</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Gaussian90</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Gaussian92</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Gaussian94</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Gaussian95</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>Gaussian98</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>Ghemical Quantum/Molecular Mechanics Model</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>Ghemical Simplified Protein Model</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>HyperChem HIN</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>IUPAC-NIST Chemical Identifier (Plain Text)</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>IUPAC-NIST Chemical Identifier (XML)</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>JME</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Jaguar</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>MDL Mol/SDF V3000</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>MDL Molfile</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>MDL Molfile V2000</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>MDL RXN V3000</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>MDL Reaction format</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>MDL Structure-data file</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MOPAC 2002</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MOPAC 2007</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MOPAC 2009</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MOPAC 2012</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MOPAC 93</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MOPAC 97</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MOPAC7</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MOPAC7 Input</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>MSI BGF</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>MacroModel</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>MacroModel</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Massively Parallel Quantum Chemistry Program</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>MoSS Output Format</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>Mol2 (Sybyl)</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>NWChem</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>PCModel</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>POV Ray</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Parallel Quantum Solutions</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>PolyMorph Predictor (Cerius)</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>Protein Brookhave Database (PDB)</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Protein Data Bank Markup Language (PDBML)</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>PubChem</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>PubChem Compound ASN</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>PubChem Compound XML</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>PubChem Compounds XML</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>PubChem Substance XML</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>PubChem Substances ASN</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>PubChem Substances XML</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Q-Chem</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Raw Copy</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>SMARTS</td>
</tr>
<tr>
  <td>RW</td>
  <td></td>
  <td>SMILES</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>SMILES FIX</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Scalable Vector Graphics</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>ShelXL</td>
</tr>
<tr>
  <td></td>
  <td>M</td>
  <td>Spartan Quantum Mechanics Program</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Sybyl descriptor</td>
</tr>
<tr>
  <td>RW</td>
  <td>M</td>
  <td>Symyx Rgroup query files</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Tinker MM2</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Tinker XYZ</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>TurboMole</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>UniChemXYZ</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>VASP</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Viewmol</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>XED</td>
</tr>
<tr>
  <td>RW</td>
  <td></td>
  <td>XYZ</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Yasara</td>
</tr>
<tr>
  <td>R</td>
  <td>M</td>
  <td>ZMatrix</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>Zindo</td>
</tr>
</table>

## The Readers and Writers

Additionally, for all formats we can list information about the readers and writers, again
by iterating over all formats:

**Script** [code/ListAllIOClassesByFormat.groovy](code/ListAllIOClassesByFormat.code.md)
```groovy
for (format in formats) {
  if (format instanceof IChemFormat &&
      (format.getReaderClassName() != null ||
       format.getWriterClassName() != null)) {
    output.append(
      "## " + format.formatName + "\n"
    )
    // output some further format details
    if (format.readerClassName != null) {
      reader = format.readerClassName.substring(
        format.readerClassName.lastIndexOf(".") + 1
      )
      output.append(
        "### " + reader + "\n"
      )
    }
    if (format.writerClassName != null) {
      writer = format.writerClassName.substring(
        format.writerClassName.lastIndexOf(".") + 1
      )
      output.append(
        "### " + writer + "\n"
      )
    }
  }
}
```

<input>ioclasseslist.md</input>