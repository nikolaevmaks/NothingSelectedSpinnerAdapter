# NothingSelectedSpinnerAdapter


How to use

Use NothingSelectedSpinnerAdapter's setSelection instead of setSelection in Spinner.
NothingSelectedSpinnerAdapter's setSelection allows -1 position index (nothing selected).

Simple example

```java
private static class DocumentAdapterItem {
	String name;
	
	DocumentAdapterItem(String name, DocumentType documentType) {
		this.name = name;
    	}
}


private class DocumentAdapter extends NothingSelectedSpinnerAdapter<DocumentAdapterItem> {

	private List<DocumentAdapterItem> mDocuments = new ArrayList<>();

	DocumentAdapter(Spinner spinner) {
		super(spinner);
	}

	void update(List<DocumentAdapterItem> documents) {
		mDocuments = documents;
		notifyDataSetChanged();
	}

	@Override
	protected String getNothingSelectedText(DocumentAdapterItem nothingSelectedDataItem) {
		return nothingSelectedDataItem.name;
	}
	// when only text as nothing selected item required
	@Override
	protected String getNothingSelectedText(DocumentAdapterItem nothingSelectedDataItem) {
		return "default document number";
	}

	@Override
	protected String getDataItemText(int position) {
		return getDataItem(position).name;
	}

	@Override
	protected int getDataItemCount() {
		return mDocuments.size();
	}

	@Override
	public DocumentAdapterItem getDataItem(int position) {
		return mDocuments.get(position);
	}
}
	
	
@Override
public void onCreate(Bundle savedInstanceState) {
  mDocumentAdapter = new DocumentAdapter(mSpinnerDocument);

  mDocumentAdapter.setNothingSelectedDataItem(new DocumentAdapterItem("default document number");
  
  // now "default document number" data item is setted as nothing selected item
  mDocumentAdapter.setSelection(-1);
  
  mSpinnerDocument.setAdapter(mDocumentAdapter);
}
```
