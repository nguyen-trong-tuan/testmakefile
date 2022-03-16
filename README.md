# testmakefile

.PHONY: all, install, clean    
 TARGET:=sum  
 -include ./src/src.mk  
 CSRCS+= main.c  
 OBJSDIR=./build  
 OBJS:= $(patsubst %.cpp, $(OBJSDIR)/%.o, $(CPPSRCS))  
 OBJS+= $(patsubst %.c, $(OBJSDIR)/%.o, $(CSRCS))  
 INCDIR+= -I./src  
 CFLAGS += -DDEBUG -Wall -g  
 LDFLAGS += -L./lib -lm  
 CC:= gcc  
 CXX:= g++  
 all: ${TARGET}  
 ${TARGET} : $(OBJS)  
      @echo " [LINK] $@"  
      @mkdir -p $(shell dirname $@)  
      @$(CXX) $(OBJS) -o $@ $(LDFLAGS)  
 $(OBJSDIR)/%.o: %.c $(HDRS)  
      @echo " [CC]  $@"  
      @mkdir -p $(shell dirname $@)  
      @$(CC) -c $< -o $@ $(CFLAGS) ${INCDIR}  
 $(OBJSDIR)/%.o: %.cpp $(HDRS)  
      @echo " [CXX] $@"  
      @mkdir -p $(shell dirname $@)  
      @$(CXX) -c $< -o $@ $(CFLAGS) ${INCDIR}  
 install:  
      cp -rf ${TARGET} /usr/local/bin      
 clean:  
      rm -rf ${OBJSDIR}  
      rm -rf ${TARGET}  
