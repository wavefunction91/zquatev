add_library(zquatev STATIC blocked.cc transpose.cc unblocked.cc zquatev.cc)

if( _HAS_MKL )
  target_compile_definitions( zquatev PUBLIC HAVE_ZGEMM3M )
  target_compile_definitions( zquatev PUBLIC HAVE_MKL )
endif()

if( LA_LINK )
  target_link_libraries( zquatev PUBLIC ${LA_LINK})
endif()


install(TARGETS zquatev DESTINATION lib)
