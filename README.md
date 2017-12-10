---
XML
---
Study Notes : https://www.tutorialspoint.com/xml/ , https://www.w3schools.com/xml/

XML Declaration
	
	<?xml version = "1.0" encoding = "UTF-8"? standalone="yes">
	
	version
	
	* if Declaration is not avaiable, is assume to xml verison = 1.0 
	* in case of xml verison = 1.1, it is mandatory to have declaration.
	
	encoding
	
	* How are unicode characters represented
		Example : ASCII, UTF-8, UTF-16, ISO-8859-1
			
	ASCII 
		
	8 bit of char, can only represent 128 characters, does not handle internation characters
	
	UTF-8/UTF-16
	
	* can represent internation characters.
	* UTF-8 is mac/Linux/HTML5 default
		- It is varible size encoding, multiple of 8-Byte use to represent data 
		- Any characters can be represent by UTF-8
		- Disadvantage:sometime more byte needed to represent data as compare to UTF-16
		- because it is default in most the case, always use this encoding unless you have strong
			reason to so.
	* UTF-16 is windows default
	
	
	Syntax Rules for XML Declaration
	
	* The XML declaration is case sensitive and must begin with "<?xml>" 
		where "xml" is written in lower-case.
	* If document contains XML declaration, then it strictly needs to be 
		the first statement of the XML document.
	* The XML declaration strictly needs be the first statement in the XML document.
		An HTTP protocol can override the value of encoding that you put in the XML declaration.
		
Tags/Elements/Nodes

	* Element Syntax : <element>....</element> or <element/>
	* Nesting of Elements : <contact-info><company>TutorialsPoint</company><contact-info>
	* Root Element : An XML document can have only one root element
	* Case Sensitivity : <contact-info> is different from <Contact-Info>

XML Attributes

	* Attribute names in XML (unlike HTML) are case sensitive.
	* Same attribute cannot have two values in a syntax.
	* Attribute names are defined without quotation marks, 
		whereas attribute values must always appear in quotation marks.
		<a b = "x" c = "y">....</a>
		
XML References
	
	Entity References: &amp; 
	Character References: &#65;
	

CDATA Sections

	The predefined entities such as &lt;, &gt;, and &amp; require typing and are generally 
	difficult to read in the markup. In such cases, CDATA section can be used. 
	By using CDATA section, you are commanding the parser that the particular section of the 
	document contains no markup and should be treated as regular text.
	
	CDATA Start section − <![CDATA[
	CDATA End section − ]]>
	CData section - haracters between these two enclosures are interpreted as characters, 
					and not as markup. This section may contain markup characters (<, >, and &), 
					but they are ignored by the XML processor.
	Example:
	
	<sometext>
		<![CDATA[ They're saying "x < y" & that "z > y" so I guess that means that z > x ]]>
	</sometext>

	
	
-----------------------------------
DTD : XML Document Type Declaration
-----------------------------------

	DTDs check vocabulary and validity of the structure of XML documents against grammatical 
	rules of appropriate XML language.An XML DTD can be either specified inside the document, 
	or it can be kept in a separate document and then liked separately.
	<!DOCTYPE element DTD identifier
	[
	   declaration1
	   declaration2
	   ........
	]>


Internal DTD
	
	standalone attribute in XML declaration must be set to yes.
	<!DOCTYPE root-element [element-declarations]>
	
	Example
	
		<?xml version = "1.0" encoding = "UTF-8" standalone = "yes" ?>
		<!DOCTYPE address [
		   <!ELEMENT address (name,company,phone)>
		   <!ELEMENT name (#PCDATA)>
		   <!ELEMENT company (#PCDATA)>
		   <!ELEMENT phone (#PCDATA)>
		]>

		<address>
		   <name>Tanmay Patil</name>
		   <company>TutorialsPoint</company>
		   <phone>(011) 123-4567</phone>
		</address>
	
External DTD
	
	* standalone attribute in the XML declaration must be set as no.
	* <!DOCTYPE root-element SYSTEM "file-name">

	Example:
		<?xml version = "1.0" encoding = "UTF-8" standalone = "no" ?>
		<!DOCTYPE address SYSTEM "address.dtd">
		<address>
		   <name>Tanmay Patil</name>
		   <company>TutorialsPoint</company>
		   <phone>(011) 123-4567</phone>
		</address>
		
	address.dtd
		<!ELEMENT address (name,company,phone)>
		<!ELEMENT name (#PCDATA)>
		<!ELEMENT company (#PCDATA)>
		<!ELEMENT phone (#PCDATA)>
			
		
---------------------------
XML Schema Definition (XSD)
---------------------------
	It is used to describe and validate the structure and the content of XML data. 
	XML schema defines the elements, attributes and data types.
	
	* XML work as contract for xml document. So two application know how to communicate based on contract.
	* XML follow XSD called valid xml.
	
	* Define Namespace : targetNamespace="http://www.bharatthippireddy.com/Patient"
	* aliase of Name Space: xmlns:tns="http://www.bharatthippireddy.com/Patient
	* Using name space in XML <tns:patient xmlns:tns="http://www.bharatthippireddy.com/Patient"
		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://www.bharatthippireddy.com/Patient Patient.xsd " id="123">
	
	
	
	<?xml version = "1.0" encoding = "UTF-8"?>
	<xs:schema xmlns:xs = "http://www.w3.org/2001/XMLSchema">
	   <xs:element name = "contact">
		  <xs:complexType>       <!-- ComplexType -->
			 <xs:sequence>		 <!-- Sequence -->
				<xs:element name = "name" type = "xs:string" />
				<xs:element name = "company" type = "xs:string" />
				<xs:element name = "phone" type = "xs:int" />
			 </xs:sequence>
		  </xs:complexType>
	   </xs:element>
	</xs:schema>
	
Elements
	<xs:element name = "x" type = "y"/>
	
Definition Types

	Simple Type
		Simple type element is used only in the context of the text. 
		Some of the predefined simple types are: xs:integer, xs:boolean, xs:string, xs:date.
		<xs:element name = "phone_number" type = "xs:int" />
	
	Complex Type
		A complex type is a container for other element definitions.
	
	Global Types
		With the global type, you can define a single type in your document, 
		which can be used by all other references.
		
		<xs:element name = "AddressType">
		   <xs:complexType>
			  <xs:sequence>
				 <xs:element name = "name" type = "xs:string" />
				 <xs:element name = "company" type = "xs:string" />
			  </xs:sequence> 
		   </xs:complexType>
		</xs:element>
		
		<xs:element name = "Address1">
		   <xs:complexType>
			  <xs:sequence>
				 <xs:element name = "address" type = "AddressType" />
				 <xs:element name = "phone1" type = "xs:int" /> 
			  </xs:sequence> 
		   </xs:complexType>
		</xs:element> 

		<xs:element name = "Address2">
		   <xs:complexType>
			  <xs:sequence>
				 <xs:element name = "address" type = "AddressType" />
				 <xs:element name = "phone2" type = "xs:int" /> 
			  </xs:sequence> 
		   </xs:complexType>
		</xs:element>
		
Attributes

	<xs:attribute name = "x" type = "y"/>
	
---------------------------
JAXB
---------------------------

Like ORM 
	Java <==> Hibernate <==> SQL
	Java <==> JAXB <==> XML

	* XML Schema   ---- xjc (schema compiler) ---->  Java Classes
	* Java Classes -------- schemagen ---------> Xml Schema
	* xjc and schemagen both are part of java jdk
	* Java Object <--- JAXB(Runtime Api) ---> XML  
	
JAXB 
	* Marshall
	* UnMarshall
	* Annotations
	* Apache-CFX : Java Also provide Specification	So 3rd party lib like Apache-CFX provide implementation 
	* Genrating XML file from XSD, We can use jdk tool or org.jvnet.jaxb2.maven2 maven plugin
	* Use to include global rules
		<bindingIncludes>
			<include>global.xjb</include>
		</bindingIncludes>
	
	* Use Maven generate-sources to generate java files
		<build>
			<plugins>
				<plugin>
					<groupId>org.apache.maven.plugins</groupId>
					<artifactId>maven-compiler-plugin</artifactId>
					<version>3.2</version>
					<configuration>
						<source>1.8</source>
						<target>1.8</target>
					</configuration>
				</plugin>
				
				<plugin>
					<groupId>org.jvnet.jaxb2.maven2</groupId>
					<artifactId>maven-jaxb2-plugin</artifactId>
					<version>0.9.0</version>
					<executions>
						<execution>
							<goals>
								<goal>generate</goal>
							</goals>
						</execution>
					</executions>

					<configuration>
						<schemaDirectory>${project.basedir}/src/main/xsd</schemaDirectory>
						<schemaIncludes>
							<include>Patient.xsd</include>
						</schemaIncludes>
						<bindingDirectory>${project.basedir}/src/main/xsd</bindingDirectory>
						<bindingIncludes>
							<include>global.xjb</include>
						</bindingIncludes>
						<generateDirectory>${project.basedir}/src/generated</generateDirectory>
					</configuration>
				</plugin>
			</plugins>
		</build>
	* Java
	
		try {
			JAXBContext context = JAXBContext.newInstance(Patient.class);
			Marshaller marshaller = context.createMarshaller();

			Patient patient = new Patient();
			patient.setId(123);
			patient.setName("Bharath");

			StringWriter writer = new StringWriter();
			marshaller.marshal(patient, writer);

			System.out.println(writer.toString());

			Unmarshaller unMarshaller = context.createUnmarshaller();

			Patient patientResult = (Patient) unMarshaller.unmarshal(new StringReader(writer.toString()));
			System.out.print(patientResult.getName());

		} catch (JAXBException e) {
			e.printStackTrace();
		}
	