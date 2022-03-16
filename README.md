# testmakefile

.PHONY: all, install, clean    
 TARGET=sum  
 HDRS+= sum.h  
 CSRCS+= main.c sum.c  
 CPPSRCS+=    
 OBJSDIR=./build  
 OBJS:= $(patsubst %.cpp, $(OBJSDIR)/%.o, $(CPPSRCS))  
 OBJS+= $(patsubst %.c, $(OBJSDIR)/%.o, $(CSRCS))  
 CFLAGS += -I./include -DDEBUG -Wall -g  
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
      @$(CC) -c $< -o $@ $(CFLAGS)  
 $(OBJSDIR)/%.o: %.cpp $(HDRS)  
      @echo " [CXX] $@"  
      @mkdir -p $(shell dirname $@)  
      @$(CXX) -c $< -o $@ $(CFLAGS)  
 install:
      cp -rf ${TARGET} /usr/local/bin   
 clean:  
      rm -rf ${OBJSDIR}/*.o  
      rm -rf ${TARGET}  
