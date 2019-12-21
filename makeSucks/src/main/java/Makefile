include MakefileInclusion

projectRoot := ../../..
targetDirectory := ${projectRoot}/target
makeSucksEntities := ${projectRoot}/../makeSucks-entities/target/classes
classesDirectory := ${targetDirectory}/classes
sources := ${call recursiveFilter,,%.java}
knownClasses := ${sources:%.java=${classesDirectory}/%.class}

#To contain appended sources that have changed.  Appending inserts a preceeding space character.
changedSources :=

#Compiles Java classes.
all: ${knownClasses} | ${classesDirectory}
	${if ${changedSources},\
		@javac -cp ${classesDirectory}:${makeSucksEntities} -d ${classesDirectory} ${strip ${changedSources}}\
	}

#Captures Java source files that have changed.
${classesDirectory}/%.class: %.java
	${eval changedSources += $$<}

#Creates the output directory for Java classes.
${classesDirectory}:
	@mkdir -p ${classesDirectory}

#Removes all output.
Clean:
	@rm -f -r ${targetDirectory}
