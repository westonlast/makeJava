include MakefileInclusion

targetDirectory := ../../../../target
classDirectory := ${targetDirectory}/classes
xjcDirectory := ${targetDirectory}/generated-sources/xjc
classpath := ${subst /,.,${packageDirectory}}
packageDirectories := ${foreach schema,${schemas},${classDirectory}/${packageDirectory}/${getLowercaseBasename}}

#Creates all class output directories.
all: ${packageDirectories}

#Maps Java class output directories to JAXB Java output directories.
${classDirectory}/${packageDirectory}/%: ${xjcDirectory}/${packageDirectory}/% | ${classDirectory}
	@javac -d ${classDirectory} $</*

#Creates the output directory for the Java compiler.
${classDirectory}:
	@mkdir -p ${classDirectory}

#Maps each lowercase package structure directory to the mixed case input file.
define lowercaseToMixedTemplate
${xjcDirectory}/${packageDirectory}/${getLowercaseBasename}: ${schema} | ${xjcDirectory}
	@xjc -nv -p ${classpath}.$${notdir $$@} -d ${xjcDirectory} ${schema}
endef

#Creates a target for each output directory to input file mapping.
${foreach schema,${schemas},${eval ${lowercaseToMixedTemplate}}}

#Creates the output directory for the JAXB XML Schema compiler.
${xjcDirectory}:
	@mkdir -p ${xjcDirectory}

#Removes all output.
Clean:
	@rm -f -r ${targetDirectory}
