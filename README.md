# NothingSelectedSpinnerAdapter

Related StackOverflow question (http://stackoverflow.com/questions/867518/how-to-make-an-android-spinner-with-initial-text-select-one)

###How to use

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

	// override when only nothing selected data item is required (not simple text)
	@Override
	protected String getNothingSelectedText(DocumentAdapterItem nothingSelectedDataItem) {
		return nothingSelectedDataItem.name;
	}
	// override when only text as nothing selected item is required
	@Override
	protected String getNothingSelectedText() {
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
  
  // now "default document number" data item is set as nothing selected item
  mDocumentAdapter.setSelection(-1);
  // OR first item in data items is default selected item
  mDocumentAdapter.setSelection(0);
  
  mSpinnerDocument.setAdapter(mDocumentAdapter);
}
```
